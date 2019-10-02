Title: On-Premise CloudWatch Metrics with AWS CLI
Date: 2019-10-02 21:16
Category: General
Tags: code, work
Slug: cloud watch-metrics-aws-cli
Subtitle: Who will watch the watchmen?

![Have you tried AWS CLI?]({filename}/images/aws-cli.jpg)

CloudWatch is pretty cool, and looking at a metrics dashboard and setting up
alarms is pretty badass—especially when you're not a full-time DevOps and
don't have the time to worry about your _monitoring solution_ in addition to
the thing it's _supposed_ to look after.

If you're running some of your stuff outside AWS (cue gasps), [CloudWatch agent][1]
is supposed to have you covered, but after following the instructions to a
tee, I found that it wasn't doing what it said on the tin, and the agent was
refusing to start up[^1].

Anyhoo, I was running out of time and I absolutely had to get this very simple
metric into CloudWatch, and after 2 days of losing sleep and trying to make
the agent work, I gave up. Thankfully, the ever reliable [AWS CLI][2] was
there to pick me up.

It turns out a simple `aws cloudwatch put-metric-data` is all you need to push
metrics to CloudWatch. There's actually [an entire doc on it][3], which I only
found while writing this post.

### The Setup

You need to make sure you have a IAM role set up with the ability to push
metrics to CloudWatch, which is [covered in the CloudWatch agent docs][4].

For my setup, I just wanted to send the disk utilisation to CloudWatch, so I
created a shell script that looked like this:

```bash
#!/bin/bash

freeSpace=`df -m | awk 'NR==2{print $4}'`
/usr/local/bin/aws cloudwatch put-metric-data --metric-name my-server-FreeDisk --value $freeSpace --unit Megabytes --namespace my-server --profile AmazonCloudWatchAgent
```

Here, I am using the `--profile` flag to select the correct IAM user, which has
been added to my AWS `credentials` and `config` files.

The shell script was simply called every 5 minutes from a cron job, and I had the
whole setup up and running in no time. You can do fancy stuff like sending in
entire JSON files, which will come in handy if you want to work with Docker stats etc.

[^1]: Some issue about the instance not having an EC2 identifier, which—_duh_

[1]: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/install-CloudWatch-Agent-on-premise.html
[2]: https://aws.amazon.com/cli/
[3]: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html
[4]: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-iam-roles-for-cloudwatch-agent.html
