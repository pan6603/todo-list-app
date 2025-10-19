## UI 생성

### 실습 코드 

App.tsx
```
import './App.css'
import Todoform from './componets/Todoform'
import TodoItem from './componets/TodoItem'

function App() {


  return (
    <>
      <h1>Todo List</h1>
      <Todoform />
      <hr />
      <ul>
        <TodoItem />
      </ul>
    </>
  )
}

export default App

```
+ import 통해서 Todoform와 TodoItem 가져온다.


Todoform.tsx
```
export default function Todoform() {
    return (
        <form>
            <input type="text" placeholder="할일을 입력해주세요."/>
            <input type="date"/>
            <button>추가</button>
        </form>
    )
}
```
+ 텍스트 input 만들기
+ 날짜 input 만들기 

TodoItem.tsx
```
export default function TodoItem() {
    return (
        <li>Todo Title</li>
    )
}
```
  

### 메모 정리 
+ UI 먼저 만들다.
+ index.css > body 안에 place-items를 지운다. 
