Title: Go යොදාගෙන සරළ version checker එක​ක්
Date: 2019-12-16 21:08
Category: General
Tags: code, golang, sinhala
Slug: a-simple-version-checker-in-go
Lang: si

![Version Check එ​ක]({filename}/images/version-output.png)

දැනට මම ඉන්න වැඩපොලේ සයිට් 15ක විතර version ට්‍රැක් කරගෙන යාවත්කාලීන
කරන්න අවශ්‍යතාවයක් තියනව. අපි ඕක automate කරගන්න සරළ Go මෘදුකාංගයක්
ලියාගත්ත. ඒකෙ කතාව තමයි මේ...

ලයිව් සයිට් එකේ පාවිච්චි කරන කෝඩ් එකට වඩා පොඩ්ඩක් මේක සරළ කරලයි
තියෙන්නෙ, ඒත් මූලික ක්‍රියාවලිය එකමයි. සයිට් වල තියෙන generator මෙටා ටැග්
කියවන එක තමයි මේකෙ​න් වෙන්නෙ[^1]. Go වල තියෙන Goroutines කියන සමාන්තරව
වැඩ ගොඩක් කරගන්න පුළුවන් විශේෂාංගය තමයි මේකට අපි පාවිච්චි කරේ.

```go
package main

import (
	"encoding/json"
	"io/ioutil"
	"net/http"
	"os"
	"regexp"
	"time"
)

// Site type holds information about sites
type Site struct {
	Name, URL, Version, TimeTaken string
}

var sites = []Site{
	{"Site A", "https://a.web.site", "N/A", ""},
	{"Site B", "https://b.web.site", "N/A", ""},
	{"Site C", "https://c.web.site", "N/A", ""},
}

// Parser type holds information about the parsing
type Parser struct {
	url, body string
}

func (p *Parser) setURL(url string) {
	p.url = url
	p.body = ""
}
```

`Site` කියන්නෙ සයිට් එක එක ගැන දත්ත ටික තියාගන්න struct එකක්. මේකෙම පස්සෙ
පුරෝගන්න version එකයි දත්ත ටික් රික්වෙස්ට් කරල ලබාගන්න ගිය වෙලාවයි දාන්නත් ඉඩ
තියාගෙන තියෙනව.[^2].

සයිට් ගොඩක් තිය​න slice එකක් අපි හදල ඒකෙ ත​තු ලබාගන්න ඕනෙ සයිට් ටිකේ URL ටික
දාගන්නව.

`Parser` එක තියෙන්නෙ දත්ත ලබාගන්නයි ලබාගත්ත දත්ත ඇතුළෙන් අපිට ඕනෙ version
නොම්බරේ ලබාගන්න එකයි කරන්න. හැම සයිට් එකකටම අලුත් parser එකක් අපි පාවිච්චි
කරනව. Parser එකේ තව මෙත​ඩ් දෙකකුත් තියෙනව: 

```go
func (p *Parser) getMatches(regexString string, index int) string {
	regex, _ := regexp.Compile(regexString)

	matches := regex.FindStringSubmatch(p.body)
	if len(matches) == index+1 {
		return matches[index]
	}

	return "N/A"
}

func (p *Parser) getVersion() string {
	res, err := http.Get(p.url)
	if err != nil {
		return "Fetch Error"
	}

	body, err := ioutil.ReadAll(res.Body)
	res.Body.Close()
	if err != nil {
		return "Parse Error"
	}

	p.body = string(body)
	return p.getMatches("(<meta name=\"generator\" content=\")([^\"]+)", 2)
}
```

`getVersion()` එකෙන් වෙබ් පිටුවෙ අන්තර්ගතය ලබාගන්න එක තම​යි වෙන්නෙ. `getMatches()`
එකෙන් තමයි regular expression (regex) එකක් පාවිච්චි කරල generator tag එක අල්ලගෙන
ඒකෙන් අපිට ඕනෙ version නොම්බරේ ලබාගන්නෙ.

අනිතිමටම තියෙන​ව main function එක​යි `getSiteVersion()` goroutine එක​යි:

```go
func getSiteVersion(key int, done chan<- bool) {
	start := time.Now() // to check the time taken

	site := Parser{}
	site.setURL(sites[key].URL)
	sites[key].Version = site.getVersion()
	sites[key].TimeTaken = time.Since(start).String()

	done <- true
}

func main() {
	done := make(chan bool)
	for index := range sites {
		go getSiteVersion(index, done)
	}

	for i := 0; i < len(sites); i++ {
		<-done
	}

	enc := json.NewEncoder(os.Stdout)
	enc.Encode(sites)
}
```

`getSiteVersion()` එක ලූප් එකක් ඇතුළෙ කෝල් වෙනව. ඒකෙන් අලුත් Parser එකක් හැදිල,
පේජ් එකේ අන්තර්ගතය අරන්, version නොම්බරේ හොයාගෙන, ඔක්කොටම ගතවෙච්ච කාලෙත්
සටහන් කරගන්නව. මේකෙ [mutex][1] එකක් අපි පාවිච්චි කරන්නෙ නෑ මොකෝ `sites` slice
එක පාවිච්චි කරද්දි හැම slice element එකම කියවන්නෙයි ලියන්නෙයි ඒකට අදාල Goroutine
එකෙන් විතරක් නිසා. එහෙම නොවුනනම් අනිවා mutex එකක් පාවිච්චි කරන්න වෙනව.

`main()` එකේ `done` කියල channel එකක් අපි පාවිච්චි කරනව. ඒ program එක ඉවර කරන්න
කලිං ඔක්කොම Goroutines ටික වැඩ ඉවරයි නේද කියල චෙක් කරන්න. මේ වෙනුවට
[WaitGroup][2] එකක් පාවිච්චි කරන්නත් පුලුවන්. අන්තිමට අපි `sites` slice එක JSON එකක්
විදිහට එළියට දානව.

රස්සාව <s>වෙලා​වෙ</s> වෙනුවෙන් ලියපු එකම Go කෝඩ් කෑල්ල මේක තමයි. තව ලියන්න
තිබ්බ නං කියල හිතෙනව, එච්චරට language එක ලස්සනයි. මේ වගේ systems වැඩ කරන්න
එහෙම කියාපු language එක.

[**මුලු කෝඩ් එකම Github එකේ තියෙනව.**][3]

[^1]: ඕපන් සෝස් සොෆ්ට්වෙයාර් වල එහෙමනම් මෙහෙම එලිපිට වර්ශන් එක දාන එක
අවුලක් වෙන්න පුළුවන්, මොකෝ known bugs පාවිච්චි කරල හැකර් අයියල සයිට් එකට
බහින්න ඉඩ තියෙන නිසා.

[^2]: සයිට් එකේ response times එහෙම අවුල්ද කියල බලාගන්න මේක උදව් වෙනව.

[1]: https://gobyexample.com/mutexes
[2]: https://gobyexample.com/waitgroups
[3]: https://gist.github.com/janithl/a7c7369785c0b7b26c17f7a2673f8bea
