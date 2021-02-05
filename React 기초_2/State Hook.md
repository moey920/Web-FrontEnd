# Hook과 함수형 컴포넌트

State Hook에 대해 알아보기 전에 Hook을 사용할 수 있는 함수형 컴포넌트에 대해 짚고 넘어가겠습니다. React의 함수형 컴포넌트는 일반적으로 이렇게 생겼습니다.
```
function Example(props) {
  // 여기서 Hook을 사용할 수 있습니다!
  return <div />;
}
```

또한 아래와 같이 화살표 함수(arrow function)를 이용해 구현되었을 수도 있으며, 마찬가지로 함수형 컴포넌트입니다.
```
const Example = (props) => {
  // 여기서 Hook을 사용할 수 있습니다!
  return <div />;
}
```

함수형 컴포넌트가 state가 없는 컴포넌트로 알고 있었을 겁니다. 하지만 Hook은 React state를 함수 안에서 사용할 수 있게 해줍니다! 당연하겠지만 Hook은 클래스 안에서 동작하지 않기 때문에 클래스를 작성하지 않고 사용해야 합니다.

## Hook 사용하기

React의 Hook을 사용하기 위해서는 사용할 Hook을 import를 해줘야 합니다. 만약 State Hook을 사용하기 위해 useState()를 이용하고 싶다면 아래처럼 해주면 됩니다.
```
import React, { useState } from 'react';
```

Hook은 아주 특별한 함수입니다. 위에 나온 useState()는 state를 함수 컴포넌트 안에서 사용할 수 있게 해줍니다. 이제 함수형 컴포넌트를 사용하던 중 state를 추가하고 싶다면 클래스 컴포넌트로 바꿀 필요 없이 함수 컴포넌트 안에서 Hook을 이용하여 state를 사용하면 됩니다. 그 외에 여러 Hook은 나중에 살펴봅시다!
