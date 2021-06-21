Outside the component: 

```tsx
export const debounce = (func: <T>(args?: T) => void, wait: number) => {
  let timeout: NodeJS.Timeout

  return <T>(args?: T) => {
    clearTimeout(timeout)
    timeout = setTimeout(() => {
      clearTimeout(timeout)
      func(args)
    }, wait)
  }
}
```

## With `useRef`


```tsx
const debouncedFn = useRef(debounce(myFn, 1000)).current
```

Works nicely with functions that don't interact with state and don't receive parameters. `myFn` is evaluated only once (at creation).

`useRef` creates a mutable object whose `current` value only changes if we do it. If we don't change it, the value will be the same throughout the lifetime of the component.


## With `useMemo`

```tsx
const debouncedFn = useMemo(() => debounce(myFn, 1000), [myFn])
```

Works nicely with functions that interact with states. Just list the correct dependencies.

Using `useMemo` here instead of `useCallback` because we want React to run the function, generating the debounced one. `useCallback` would return a function that creates a debounced function, and we want to create a debounced function only once. `useMemo` does that, it runs the function that creates a debounced function.

