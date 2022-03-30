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

### 2. 항목 추가 기능 구현하기

> TodoInsert 컴포넌트에서 인풋상태를 관리하고 App 컴포넌트에는 todos 배열에 새로운 객체를 추가하는 함수를
> 생성해주어야함

1. useState를 사용하여 value라는 상태를 정의
2. input에 넣어줄 onChange 함수를 작성
    - 컴포넌트가 리렌더링될 때마다 함수를 새로 만드는 것이 아닌, 한 번 함수를 만들고 재사용할 수 있도록 `useCallback` Hook을 사용
3. todos 배열에 새 객체 추가를 위해 App 컴포넌트에서 todos 배열에 새 객체를 추가하는 onInsert 함수 생성
    - id 값은 `useRef`를 사용하여 관리
      **(id값은 렌더링되는 정보가 아니기 때문에 리렌더링될 필요가 없어서 useRef를 사용)**
    - 성능을 아낄 수 있도록 useCallback으로 감싸주기
      **(props로 전달해야할 함수를 만들 때는 useCallback을 사용하여 함수를 감싸주는 것을 습관화 해야함)**
4. onInsert함수를 만든 뒤에는 해당 함수를 TodoInsert 컴포넌트의 props로 설정
5. TodoInsert에서 받아온 onInsert 함수를 현재 useState를 통해 관리하고 있는 value 값을 파라미터로 넣어서 호출
6. onSubit 이라는 함수를 만들고, 이를 form의 onSubmit으로 설정
    - 이 함수가 호출되면 props로 받아 온 onInsert 함수에 현재 value 값을 파라미터로 넣어서 호출하고, 현재 value 값을 초기화함
    - onSubmit 이벤트는 브라우저를 새로고침 시키기 때문에 `e.preventDefault()` 함수를 호출하여 새로고침을 방지
    - onSubmit 대신 버튼의 onClick 이벤트로도 충분히 처리 가능
