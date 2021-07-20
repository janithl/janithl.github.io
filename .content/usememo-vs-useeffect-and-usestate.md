Title: useMemo vs useEffect and useState
Date: 2021-07-20 08:48
Category: General
Tags: code, js and ts, react

Since the advent of React Hooks, there have been a few hook-related
anti-patterns that have popped up. To be fair, these existed before
hooks as well, but in different forms. The use of derived state is
one of the most pervasive of these. As the React blog pointed out
way back in 2018, [_"You Probably Don't Need Derived State"_][1].

In a hooks-based application, it may look something like this:

```js
const MyComponent = ({ initialValue }) => {
    const [value, setValue] = useState();
    useEffect(() => {
        const derivedValue = expensiveTransform(initialValue);
        setValue(derivedValue);
    }, [initialValue]);

    ...
}
```

There are two derivations of this, one where the value is updated by
the user inside the component, and another where this `value` is used
but not updated.

For the first type, consider how any update of `initialValue` will
overwrite the changes made by the user in the state. Do you really
want this to happen? The blog post I linked to above lays out a few
alternatives.

For the second type, there is **no need** to put things in state anyway
if you don't plan on updating it. You can simply assign it to a constant:

```js
const MyComponent = ({ initialValue }) => {
    const derivedValue = expensiveTransform(initialValue);
    ...
}
```

Or, if you're worried about the `expensiveTransform()` and wish to avoid
unnecessarily calling it, you can use memoization:

```js
const MyComponent = ({ initialValue }) => {
    const derivedValue = useMemo(
        () => expensiveTransform(initialValue),
        [initialValue]
    );
    ...
}
```

Simple, and saves you the trouble of dealing with unnecessary state.

[1]: https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html
