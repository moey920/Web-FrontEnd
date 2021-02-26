# 1. 카페 API 불러오기

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

# 2. 카페 API 등록하기

- ID와 메뉴 이름, 설명, 가격을 입력하고 등록하기 버튼을 클릭하면 API에 새로운 카페 메뉴가 등록됩니다.

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
            <button onClick={fetchCafe}>불러오기</button>
        </>
    );
}

export default Cafes;
```

# 3. 카페 API 검색하기

- ID를 입력하고 검색하기 버튼 클릭 시 해당 ID를 가진 카페 메뉴의 이름, 설명, 가격을 출력합니다.

```
import React, { useState } from 'react';
import axios from 'axios';

// 지시사항에 따라 출력 결과와 동일한 동작을 하는 코드를 작성하세요.
function Cafes() {
    const [cafe, setCafe] = useState('');
    const [menuId, setMenuId] = useState();
    const [item, setItem] = useState();
    const [desc, setDesc] = useState();
    const [price, setPrice] = useState();
    const [fail, setFail] = useState();
    
    async function fetchCafe() {
        const response = await axios.get(
            `https://${window.location.hostname}:8190/data`
        );
        const menuName = response.data.map(
            (menu) => (<li key={menu.id}> {menu.item} </li>)
        );
        setCafe(menuName);
    };

    async function postCafe() {
        const newMenu = {"id": menuId, "item": item, "description": desc, "price": price};
        
        try {
            const response = await axios.post(
                `https://${window.location.hostname}:8190/data`, newMenu
            );
            setFail()
        } catch(e) {
            setFail("메뉴 등록에 실패했습니다.")
        }
    };
    
    const updateId = event => {
        setMenuId(event.target.value);
    };
    const updateItem = event => {
        setItem(event.target.value);
    };
    const updateDesc = event => {
        setDesc(event.target.value);
    };
    const updatePrice = event => {
        setPrice(event.target.value);
    };
    
    return (
        <>
            <h4>카페 메뉴</h4>
            <div> {cafe} </div> 
            <button onClick={fetchCafe}>불러오기</button> <br/><br/>
            <p>
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ID: &nbsp;
            <input value={menuId} onChange={updateId} />
            </p>
            <p>
            카페 메뉴: &nbsp;
            <input value={item} onChange={updateItem} />
            </p>
            <p>
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;설명: &nbsp;
            <input value={desc} onChange={updateDesc} /> <br/>
            </p>
            <p>
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;가격: &nbsp;
            <input value={price} onChange={updatePrice} />
            </p>
            <button onClick={postCafe}>등록하기</button> 
            <div> {fail} </div>
            <br/><br/>
        </>
    );
    

}

export default Cafes;
```

