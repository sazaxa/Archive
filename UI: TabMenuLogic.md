
1. 문제점

- UI library를 사용하던 중 원하던대로 로직을 작동할 수 없는 문제. (onClick 등이 막힘)

2. 문제의 해결

- UI library를 버리고 css를 통해 UI library의 로직을 구현해 해결할 수 있다.

3. 배운점

- UI library를 도입하기 전에 도입가능한지 아닌지를 판단하자.

4. 느낀점

- library를 보다 잘 알고 있지 않아서 생긴 문제일 수 있다는 것도 느낌


[codeSandbox](https://codesandbox.io/s/sharp-easley-214f3?file=/src/App.js:0-1269) link
```js
import react, { useState } from "react";
import styled from "styled-components";
import "./styles.css";

export default function App() {
  const TabMenu = styled.ul`
    background-color: #dcdcdc;
    font-weight: bold;
    display: flex;
    flex-direction: row;
    justify-items: center;
    align-items: center;
    list-style: none;
    .focused {
      background: red;
    }
    .submenu {
      width: 100% auto;
      padding: 15px 10px;
      cursor: pointer;
    }
  `;
  const [currentTab, setCurrentTab] = useState(0);
  const menuArr = [
    { name: "Tab1", content: "first text" },
    { name: "Tab2", content: "second text" },
    { name: "Tab3", content: "three text" }
  ];

  const selectMenuHandler = (index) => {
    setCurrentTab(index);
  };
  return (
    <div className="App">
      <TabMenu>
        {menuArr.map((v, i) => {
          return (
            <li
              key={v + i}
              className={currentTab === i ? "submenu focused" : "submenu"}
              onClick={() => selectMenuHandler(i)}
            >
              {v.name}
            </li>
          );
        })}
      </TabMenu>
      <div>
        <h1>{menuArr[currentTab].content}</h1>
        <p>{menuArr[currentTab].content}</p>
      </div>
    </div>
  );
}
```
