# Zustand

## Official Docs
- https://zustand.docs.pmnd.rs/getting-started/introduction

Installation
```shell
npm install zustand
```
## Usages
Create the first store
`src/store/bearStore.ts`

```ts
import {create} from "zustand";

type State = {
  bears: number
}

type Action = {
  increaseBears: (num: State["bears"]) => void
  removeAllBears: () => void
}

const useBearStore = create<State & Action>((set) => ({
  bears: 0,
  increaseBears: (num: number) => set((state) => ({
    ...state,
    bears: state.bears + num
  })),
  removeAllBears: () => set((state) => ({
    ...state,
    bears: 0
  }))
}));

export default useBearStore;
```

Use the store in the tsx file
```tsx
import React from "react";
import {Button, Card} from "antd";

import useBearStore from "@/store/bearStore.ts";

const BearBox: React.FC = () => {

  // method 1
  const bears = useBearStore((state) => state.bears);
  const increaseBears = useBearStore(state => state.increaseBears);
  const removeAllBears = useBearStore(state => state.removeAllBears);

  return (
    <div className="container">
      <Card title={`Bears: ${bears}`} bordered={true}>
        <div>{Math.random()}</div>
        <div>
          <Button onClick={() => increaseBears(2)}>add bear</Button>
          <Button onClick={removeAllBears}>remove bear</Button>
        </div>
      </Card>
    </div>
  );
};

export default BearBox;
```
The second method to get states and actions from the store
```tsx
  // method 2
  const {bears, increaseBears, removeAllBears} = useBearStore();
```

