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

Works nicely with functions that don't interact with state and don't receive parameters. `myFn` is evaluated only once at creation.

```tsx
const debouncedFn = useRef(debounce(myFn, 1000)).current
```

## With `useMemo`

Works nicely with functions that interact with states. Just list the correct dependencies.

Using `useMemo` here instead of `useCallback` because we want React to run the function, generating the debounced one. `useCallback` would return a function that creates a debounced function. `useMemo` runs the function that creates a debonced function.

```tsx
const debouncedFn = useMemo(() => debounce(myFn, 1000), [myFn])
```
