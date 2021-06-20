Outside the component: 

```tsx
const debounce = (func: () => void, wait: number) => {
  let timeout: NodeJS.Timeout

  return () => {
    clearTimeout(timeout)
    timeout = setTimeout(() => {
      clearTimeout(timeout)
      func()
    }, wait)
  }
}
```

Inside the component:

```tsx
const debouncedFn = useRef(debounce(myFn, 1000)).current
```
