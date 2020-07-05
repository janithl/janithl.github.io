Title: Tagged Template Literals are Awesome!
Date: 2020-07-05 07:20
Category: General
Tags: code, design, js and ts, react
Slug: js-template-literals
Subtitle: Tagged under "better write this down before I forget"

You will often need to implement text that looks like this:

![Highlighted Text]({filename}/images/highlighted-text.png)

Now, it's fairly simple enough to do in HTML, but when you do it in React Native
it looks a bit gnarly:

```
<Text style={styles.text}>
  You’re going to <Text style={styles.highlighted}>send a message</Text> to{" "}
  <Text style={styles.highlighted}>Pingpong</Text>. Please confirm?
</Text>
```

Now, I prefer to keep strings like this in a separate file in React Native, to make
the frequent requests for text changes contained to a single file. But a complex
template string like this was impossible to store that way, until...

### Enter Tagged Template Literals

[This post by Tania Rascia][1] opened my eyes to the power of [Tagged Template Literals][2]
in JS. Seeing this example blew my mind:

```js
function bold(strings, ...expressions) {
  let finalString = "";

  // Loop through all expressions
  expressions.forEach((value, i) => {
    finalString += `${strings[i]}<strong>${value}</strong>`;
  });

  // Add the last string literal
  finalString += strings[strings.length - 1];
  return finalString;
}

const string = bold`This is a string with ${true} and ${false} and ${100} interpolated inside.`;
console.log(string);
```

Okay, with a quick few tweaks we can definitely apply this to React Native, right?

### Highlighting Text in React Native

```
const highlightText = (baseStyle, highlightStyle) => (strings, ...values) => (
  <Text style={baseStyle}>
    {strings.map((string, index) => (
      <>
        {string}
        <Text style={highlightStyle}>
          {values[index]}
        </Text>
      </>
    ))}
  </Text>
);
```

Note I am using a higher order function so that I can pass in custom styles. We can also
pass in other stuff like entire components, if that is the requirement.

Now, we could store the Tagged Template Literal and use it wherever in our JSX.

```
const action = "send a message";
const user = "Pingpong";
const description = highlightText(
  styles.text,
  styles.highlight
)`You’re going to ${action} to ${user}. Please confirm?`;

// ...app code
<Text>{description}</Text>;
```

Aaand, we're done! 🎉

---

**Edit:** Many of you will rightly wonder if `action`, `user`, and `styles` will need
to be defined in the same file as the Template Literal. No, we can simply make it a
function and pass these values direct from the component, like so:

```
const description = (user, action, styles) => highlightText(
  styles.text,
  styles.highlight
)`You’re going to ${action} to ${user}. Please confirm?`;

// ...app code
<Text>{description('Pingpong', 'Send a message', styles)}</Text>;
```

Pretty cool, right?

[1]: https://www.taniarascia.com/understanding-template-literals/
[2]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
