`MyContextComponent` is a component that holds an inner state. Through the Context API and by using hooks, we can make this internal state available outside of the component.

The way I think context is most useful, is by later making it available through a hook that can **consume** and **update** the values. To do this, we need to be smart with our types. But let's go through each step.

### 1. Create a simple component with state

```tsx
import React, { useState } from "react";

const MyContextComponent = (): JSX.Element => {
  const [myState, setMyState] = useState();
  return <div></div>;
};

export default MyContextComponent;
```

### 2. Create a ContextType

To make Typescript relax and enjoy the ride, we're gonna need a `Context` type. To be able to consume the value, we're gonna need a `value: MyData` property. And to update the value, we're gonna use the `setState` that comes with our `useState` hook. The type of that this is `React.Dispatch<React.SetStateAction<T>>`. Hence:

```tsx
type ContextType<T> = {
  value: T;
  update: React.Dispatch<React.SetStateAction<T>>;
} | null;
```

(It can also be null so you can initialize the context with something)

### 3. Create your context (outside the component)

```tsx
const MyContext = React.createContext<ContextType<MyData>>(null);
```

Now the `value` is gonna be `MyData` and `update` is gonna be a `setState` of `MyData`

### 4. Wrap the children with your Context Provider

Update Props:

```tsx
type Props = {
  children: React.ReactNode;
};
```

Add `children` to the function signature:

```tsx
const MyContextComponent = ({ children }: Props): JSX.Element
```

And wrap the children with the provider:

```tsx
<MyContextComponent.Provider>{children}</MyContextComponent.Provider>
```

### 5. Pass the props to your Provider

The context provider receives a `value` prop. In our case, the `value` is an object with a `MyData` `value` and an `update` function, so that the consumer of this context can both read and write the value.

```tsx
<MyContextComponent.Provider value={{ value: myState, update: setMyState }}>
```

### 6. To make things easier, create a hook

```tsx
export const useMyContext = (): any => {
  const myContext = useContext(MyContext);
  return [myContext?.value, myContext?.update];
};
```

Here I'm returning `any` because I'm lazy, but the return actually is the value and the update function in the same fashion in which they are returned by `useState`: `[value, setValue]`.

> Edit:
> `any` will cause a lot of problem. A good return type is this: `[MyData, React.Dispatch<React.SetStateAction<MyData>> | undefined]`. This allows you to initialize the `React.createContext()` with a value but without an update function. But this also means you'll have to make sure the function actually exists before using it, i.e. `setMyData && setMyData(newData)`

The finalized file will look something like this:

```tsx
import React, { useContext, useState } from "react";
import { MyData } from "../models/types";

type ContextType<T> = {
  value: T;
  update: React.Dispatch<React.SetStateAction<T>>;
} | null;

const MyContext = React.createContext<ContextType<MyData[]>>(null);

export const useMyContext = (): any => {
  const myData = useContext(MyContext);
  return [myData?.value, myData?.update];
};

type Props = {
  children: React.ReactNode;
};

const MyContextProvider = ({ children }: Props): JSX.Element => {
  const [myData, setMyData] = useState<MyData[]>([]);
  return (
    <MyContext.Provider value={{ value: myData, update: setMyData }}>
      {children}
    </MyContext.Provider>
  );
};

export default MyContextProvider;
```

### 7. Use it in your app

```tsx
<MyContextProvider>
  <App />
</MyContextProvider>
```

```tsx
const [myData, setMyData] = useMyContext();
```
