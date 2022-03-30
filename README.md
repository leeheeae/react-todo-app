# Todo React App

기본적인 React의 기능들을 이용하여 Todo App 만들기

## 사용한 라이브러리

`React`, `React-icons`, `node-sass`

# UI 구성하기

1. **TodoTemplate** : 일정 관리 앱의 최상위 탬플릿, 앱 타이틀, 일정관리 목록을 한 곳에 모아 보여주며, children으로 내부 JSX를 props로 받아와서 랜더링
2. **TodoInsert** : 새로운 항목을 입력하고 추가할 수 있는 컴포넌트, state를 통해 인풋의 상태를 관리
3. **TodoListItem** : 각 할 일 항목에 대한 정보를 보여주는 컴포넌트, todo 객체를 props로 받아와서 상태에 따라 다른 스타일의 UI를 보여줌
4. **TodoList** : todos 배열을 props로 받아온 후, 이를 배열 내장 함수 map을 사용해서 여러개의 TodoListItem 컴포넌트로 변환하여 보여줌

---

### App에서 Todos 상태 사용하기

1.  일정 항목에 대한 상태들은 모두 App 컴포넌트에서 관리
2.  App에서 useState를 사용하여 todos 라는 상태를 정의하고, todos를 TodoList의 props로 전달
3.  TodoList에서 props 값을 받아 온 후 TodoItem으로 변환하여 렌더링
4.  map 함수를 통해 TodoListItem으로 이루어진 배열로 변환하여 렌더링
    -   map을 사용할 때는 key props를 전달해 주어야함
    -   todo 데이터는 통째로 props로 전달
        **(여러 종류의 값을 전달해야 하는 경우에는 객체로 통째로 전달하는 편이 나중에 성능 최적화를 할 때 편리함)**
5.  조건부 스타일링을 위해 TodoListItem에서 classnames를 사용하여 작성
6.  App에서 전달해 준 todos 값에 따라 다른 내용을 제대로 보여줌
