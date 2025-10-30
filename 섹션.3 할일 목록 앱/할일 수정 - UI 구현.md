## 할일 수정 - UI 구현


App.tsx
```

import { useEffect, useState } from 'react'
import './App.css'
import type { Todo } from './types'
import Todoform from './componets/Todoform'
import TodoItem from './componets/TodoItem'
import * as S from './store';

const KEY = 'todos:v1';

function load(): Todo[]{
  const raw = localStorage.getItem(KEY)
  return raw ? (JSON.parse(raw) as Todo[]):[];
}

function save(todos:Todo[]) {
  localStorage.setItem(KEY, JSON.stringify(todos));
}

function App() {
  const [todos, setTodos] = useState<Todo[]>(() => load());

  useEffect(() => { // todos 변경되면 로컬 스토리지에 값을 저장 
      save(todos)
  },[todos])

  return (
    <>
      <h1>Todo List</h1>
      <Todoform onAdd={(title: string, due?: string)=>setTodos((prev)=> S.add(prev,{title, due}))}/>
      <hr />
      <ul>
        {todos.map((t) => 
          <TodoItem 
            todo={t} 
            key={t.id}
            onToggle={()=>{}}
            onDelete={()=>{}}
            onEdit={()=>{}}
          />
        )}
      </ul>
    </>
  )
}

export default App

```

TodoItem.tsx 
```
import { useState } from "react";
import type { Todo, TodoUpdate } from "../types"

interface Props {
    todo: Todo;
    onToggle: ()=> void;
    onDelete: ()=> void;
    onEdit: (patch: TodoUpdate)=> void;
}

export default function TodoItem({todo, onToggle, onDelete, onEdit}: Props) {
    const [editing, setEditing] = useState(false); // 수정모드 여부
    const [title, setTitle] = useState(todo.title);
    const [due, setDue] = useState<string>(todo.due ?? '')

    function saveEdit() {
        const patch:TodoUpdate = {title: title.trim(), due: due || undefined}
        onEdit(patch);
        setEditing(false);
    }

    return (
        <li>
            {!editing ? 
                <>
                    {todo.title}
                    <button onClick={()=> setEditing(true)}>수정</button>
                    <button>삭제</button>
                </>
                : 
                <>
                    <input type="text" value={title} onChange={e=>setTitle(e.target.value)}/>
                    <input type="date" value={due} onChange={e=>setDue(e.target.value)}/>

                    <button onClick={saveEdit}>저장</button>
                    <button onClick={()=> setEditing(false)}>취소</button>
                </>    
            }
            
        </li>
    )
}
```
