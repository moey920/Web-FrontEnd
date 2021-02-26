1. 카페 API 불러오기

- 불러오기 버튼 클릭 시 현재 API에 등록된 카페 메뉴의 이름을 출력합니다.

```
import React, { useState } from 'react';
import axios from 'axios';

// 지시사항에 따라 출력 결과와 동일한 동작을 하는 코드를 작성하세요.
function Cafes() {
    const [cafe, setCafe] = useState('');
    
    async function fetchCafe() {
        const response = await axios.get(
            `https://${window.location.hostname}:8190/data`
        );
        const menuName = response.data.map(
            (menu) => (<li key={menu.id}> {menu.item} </li>)
        );
        setCafe(menuName);
    };
    
    return (
        <>
            <h4>카페 메뉴</h4>
            <div id="text"> {cafe} </div> 
            <button id="button" onClick={fetchCafe}>불러오기</button>
        </>
    );
}

export default Cafes;
```


