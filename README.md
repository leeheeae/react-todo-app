# Todo React App

기본적인 React의 기능들을 이용하여 Todo App 만들기

## 사용한 라이브러리

`React`, `React-icons`, `node-sass`

# UI 구성하기

1. **TodoTemplate** : 일정 관리 앱의 최상위 탬플릿, 앱 타이틀, 일정관리 목록을 한 곳에 모아 보여주며, children으로 내부 JSX를 props로 받아와서 랜더링
2. **TodoInsert** : 새로운 항목을 입력하고 추가할 수 있는 컴포넌트, state를 통해 인풋의 상태를 관리
3. **TodoListItem** : 각 할 일 항목에 대한 정보를 보여주는 컴포넌트, todo 객체를 props로 받아와서 상태에 따라 다른 스타일의 UI를 보여줌
4. **TodoList** : todos 배열을 props로 받아온 후, 이를 배열 내장 함수 map을 사용해서 여러개의 TodoListItem 컴포넌트로 변환하여 보여줌
