# study-buddy-todo
import React, { useState } from 'react';

function App() {
  const [todos, setTodos] = useState([]); // 할 일 목록
  const [input, setInput] = useState(''); // 입력창 값

  // 할 일 추가
  const addTodo = () => {
    if (input.trim() === '') return; // 빈 문자열 무시
    setTodos([...todos, { text: input, done: false }]);
    setInput('');
  };

  // 완료 토글
  const toggleDone = (index) => {
    const newTodos = [...todos];
    newTodos[index].done = !newTodos[index].done;
    setTodos(newTodos);
  };

  // 삭제
  const deleteTodo = (index) => {
    const newTodos = todos.filter((_, i) => i !== index);
    setTodos(newTodos);
  };

  return (
    <div style={{ padding: '20px' }}>
      <h1>Todo App</h1>
      <input
        type="text"
        value={input}
        onChange={(e) => setInput(e.target.value)}
        placeholder="할 일을 입력하세요"
      />
      <button onClick={addTodo}>추가</button>
      <ul>
        {todos.map((todo, index) => (
          <li key={index}>
            <input
              type="checkbox"
              checked={todo.done}
              onChange={() => toggleDone(index)}
            />
            <span style={{ textDecoration: todo.done ? 'line-through' : '' }}>
              {todo.text}
            </span>
            <button onClick={() => deleteTodo(index)}>삭제</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
