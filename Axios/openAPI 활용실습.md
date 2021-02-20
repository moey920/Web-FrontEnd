### 포켓몬 API란?

포켓몬 API는 Pokémon 메인 게임 시리즈에 등장하는 포켓몬들에 대한 모든 것을 자세히 설명하는 API입니다.

## 포켓몬 API 특징과 구조

- HTTP GET 요청으로 API의 자원을 사용할 수 있습니다.
- 사용자가 입력한 값에 따라 포켓몬 이미지, 이름, 높이, 무게 정보를 확인할 수 있습니다.
- 만약 포켓몬 API에 없는 값 입력 시 404 에러를 반환합니다.

포켓몬 정보를 알려주는 API를 사용해서 우리는 이 중 하나의 포켓몬에 대한 정보를 읽어오는 애플리케이션을 만들어 보겠습니다. 그전에 Pokemon API<https://pokeapi.co/>의 구조를 살펴봅시다.

페이징이란 API 반환 결과를 한 번에 반환하지 않도록 나눠둔 것입니다. 위의 페이지 같은 경우 201번부터 300번까지의 검색 결과가 반환되고, 그 앞이나 뒤의 검색 결과를 가진 주소 정보를 가지고 있는 것입니다.

앞서 배웠던 Axios를 사용하여 포켓몬 OpenAPI에서 GET 요청 통해 사용자가 입력한 ID에 해당하는 포켓몬의 이름과 이미지를 표시하도록 PokéAPI를 사용해 구현할 것입니다. 그러기 위해서 아래와 같은 코드를 작성해야 합니다.
```
import axios from 'axios';

var apiUrl = "https://pokeapi.co/api/v2/pokemon/"; // API 주소
var input = document.querySelector(".pokemon-input"); // 검색할 ID
var pokemonName = document.querySelector(".pokemon-name"); // 포켓몬 이름
var pokemonImage = document.querySelector(".pokemon-image"); // 포켓몬 사진

function getPokemonData() {
    axios.get(apiUrl + input.value)
    .then(function (response) {
        pokemonName.innerHTML = response.data.forms[0].name;
        pokemonImage.src = response.data.sprites.front_default;
    })
    .catch(function (error) {
        pokemonName.innerHTML = "(An error has occurred.)";
        pokemonImage.src = "";
    });
}
var button = document.querySelector(".pokemon-button");
button.addEventListener("click", getPokemonData);
```
이때, querySelector은 index.html에 있는 태그를 지정하는 것입니다. 그리고 innerHTML과 src를 이용해 API로 반환한 값인 포켓몬의 이름과 이미지를 바로 출력합니다. innerHTML는 텍스트이고 src는 이미지의 링크를 설정하는 <img> 태그의 속성으로 해당 이미지를 출력하는 것입니다.

코드 실행 시 PokéAPI를 호출하면 Axios를 사용하여 Pokémon의 ID와 함께 API URL에 GET 요청을 보내고 결과를 반환합니다. 예를들어 입력된 ID가 25이면 전체 URL은 <https://pokeapi.co/api/v2/pokemon/25> 와 같습니다.

이 애플리케이션의 데모<https://sabe.io/demos/pokemon-api-reader>를 먼저 확인해보세요. 그리고 해당 내용을 차근차근 구현해봅시다!

### API 요청 함수 만들기 실습

axios.get()을 이용해 포켓몬 API에 요청하는 함수를 만들어봅시다. api에서 무엇을 GET 할 때는 반드시 axios.get() 형태로 가져와야 합니다.

그리고 axios.get()에 ```{ cancelToken: new axios.CancelToken(c => cancel = c) }```을 함께 넘겨줌으로써 페이지에 대한 정보가 바뀌는 것을 정리할 수 있습니다.

> cancelToken<https://xn--xy1bk56a.run/axios/guide/cancellation.html>은 Axios에서 제공하는 것으로 API 요청을 취소하는데 사용되는 토큰입니다.

useState와 useEffect를 활용하여 아래 지시사항에 따라 포켓몬의 이름들을 페이징하여 가져오는 실습을 해봅시다.

버튼 클릭 시 이동하는 부분은 Pagination.js, 포켓몬 이름 리스트를 출력하는 부분은 PokemonList.js에 구현이 되어 있습니다.
```
import React from 'react'

export default function PokemonList({ pokemon }) {
  return (
    <div>
      {pokemon.map(p => (
        <div key={p}>{p}</div>
      ))}
    </div>
  )
}
```

```
import React from 'react'

export default function Pagination({ gotoNextPage, gotoPrevPage }) {
  return (
    <div>
      {gotoPrevPage && <button onClick={gotoPrevPage}>Previous</button>}
      {gotoNextPage && <button onClick={gotoNextPage}>Next</button>}
    </div>
  )
}
```

1. src/App.js 내 useEffect 내에 axios.get()으로 currentPageUrl와 cancelToken을 함께 넘겨주세요.

2. .then()을 이용하여 API 내에 있는 모든 포켓몬 이름들을 나열하기 위한 페이징을 설정하세요.

- 로딩 설정: setLoading(false)
- 이전 페이지: setNextPageUrl(response.data.next)
- 다음 페이지: setPrevPageUrl(response.data.previous)
- url 내 포켓몬 이름 데이터: setPokemon(response.data.results.map(p => p.name))
```
import React, { useState, useEffect } from 'react';
import axios from 'axios'
import PokemonList from './PokemonList'
import Pagination from './Pagination';

function App() {
  const [pokemon, setPokemon] = useState([])
  const [currentPageUrl, setCurrentPageUrl] = useState("https://pokeapi.co/api/v2/pokemon")
  const [nextPageUrl, setNextPageUrl] = useState()
  const [prevPageUrl, setPrevPageUrl] = useState()
  const [loading, setLoading] = useState(true)


  const [] = useState()
  useEffect(() => {
    setLoading(true)
    let cancel
    
    // 포켓몬 데이터를 불러오고 cancelToken을 함께 넘겨줍니다. 그리고 state를 설정하세요.
    setLoading(false)
    axios.get(currentPageUrl, { cancelToken: new axios.CancelToken(c => cancel = c) })
    .then(function (response) {
        setNextPageUrl(response.data.next)
        setPrevPageUrl(response.data.previous)
        setPokemon(response.data.results.map(p => p.name))
    })
    
    // 페이지 이동이 취소되는 경우 현재 페이지를 유지합니다.
    return () => cancel()
  }, [currentPageUrl])

  // 다음 페이지로 이동합니다.
  function gotoNextPage() {
    setCurrentPageUrl(nextPageUrl)
  }

  // 이전 페이지로 이동합니다.
  function gotoPrevPage() {
    setCurrentPageUrl(prevPageUrl)
  }
  
  // 로딩 상태인 경우 로딩중을 출력합니다.
  if (loading) return "로딩중..."
  
  return (
    <>
      <PokemonList pokemon={pokemon} />
      <Pagination
        gotoNextPage={nextPageUrl ? gotoNextPage : null}
        gotoPrevPage={prevPageUrl ? gotoPrevPage : null}
      />
    </>
  );
}

export default App;
```

### 포켓몬 API 요청 및 예외 처리 실습

axios.get()을 이용해 포켓몬 API에 요청하는 함수 만들어 봅시다.

index.js에서 Axios를 사용하여 Pokémon의 ID와 함께 상단에 정의된 API url에 GET 요청을 보냅니다.

GET 요청 결과 반환되는 데이터를 콘솔에서 확인하고 예외 처리도 해봅시다. 예외 처리는 .then() 밑에 .catch()를 붙여 할 수 있습니다.
```
    axios.get(요청할 url)
    .then(function (response) {
        반환 결과
    })
    .catch(function (error) {
        예외 처리
    });
```

지시사항에 따라 코드를 완성해봅시다!

1. getPokemonData() 함수 내에서 입력된 ID의 포켓몬 API에 GET 요청을 하세요.
    - 포켓몬 API url은 apiUrl 변수를 이용하세요.
    - 입력된 ID는 input 변수의 값인 input.value를 이용하면 얻을 수 있습니다.
2. .then()을 이용하여 반환되는 데이터를 콘솔창에서 확인하세요.
3. .catch()를 이용하여 예외 처리를 하고 아래 코드를 추가하세요.
```
pokemonName.innerHTML = "(An error has occurred.)";
pokemonImage.src = "";
```

```
import axios from 'axios';

var apiUrl = "https://pokeapi.co/api/v2/pokemon/"; // API 주소
var input = document.querySelector(".pokemon-input"); // 검색할 ID
var pokemonName = document.querySelector(".pokemon-name"); // 포켓몬 이름
var pokemonImage = document.querySelector(".pokemon-image"); // 포켓몬 사진

function getPokemonData() {
    // 위의 선언된 변수를 활용하여 지시사항에 따라 GET 요청을 해보세요.
    axios.get(apiUrl + input.value)
    .then(function (response) {
        pokemonName.innerHTML = response.data.forms[0].name;
        pokemonImage.src = response.data.sprites.front_default;
    })
    .catch(function (error) {
        pokemonName.innerHTML = "도감에 등록되지 않은 포켓몬 번호입니다!";
        pokemonImage.src = "";
    });
}

var button = document.querySelector(".pokemon-button");
button.addEventListener("click", getPokemonData);
```


