# HOC

High Order Component is one of the key feature for `React` and in our project you can find some component is based on HOC.



Let me give some examples:

```typescript
import React, { ReactElement } from 'react';

export interface HiddenPros {
    hidden?: boolean;
}

const WithHidden = function WithHidden<P>(
    Component: React.ComponentType<P>,
): React.ComponentType<P> {
    function WithHiddenComponent(props: P & HiddenPros): ReactElement<P> {
        const { hidden } = props;
        if (hidden) {
            return <></>;
        }

        // eslint-disable-next-line react/jsx-props-no-spreading
        return <Component {...(props as P)} />;
    }

    return WithHiddenComponent;
};

export default WithHidden;
```

The code above is the hidden HOC, the input and output is component function and when property contains hidden, it just return null. This small example show that HOC could do preprocess for the component component.



If we understand that, we could abstract lots of common function and event base on HOC.&#x20;

