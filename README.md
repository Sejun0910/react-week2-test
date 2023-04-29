### [과제] 숙련주차 과제 답

- 추가하기 버튼을 클릭해도 추가한 아이템이 화면에 표시되지 않음.

해결 방법 : 제일먼저 dispatch 함수를 불러왔고
form.jsx에서 addtodo 액션을 dispatch를 해야하는 부분이 없어서
dispatch에 addtodo를 추가했다


- 추가하기 버튼 클릭 후 기존에 존재하던 아이템들이 사라짐.

해결 방법 : todos.js에 리듀서 부분에
case ADD_TODO에서 return할때 todos: [action.payload] 이 부분을
[...state.todos, action.payload] 이렇게 수정해주었다
그러면 이제 내가 입력한 값이 저장되있는 todos를 출력해준다



- 삭제 기능이 동작하지 않음.

해결 방법 : 
  // 삭제컴포넌트
  const onDeleteTodo = (id) => {
    const todo = todos.filter(item => item.id !== id)
    dispatch(deleteTodo(todo));
  };
-> 이 부분에서 const todo = todos.filter(item => item.id !== id) 이부분을 추가했다
todos에서 id값이 파라미터로 전달된 id랑 같지 않은 값만 todo에 넣어줬다
그리고 마지막에 dispatch(deleteTodo(todo)); 이 부분에서 (todo)부분을 수정했다 원래는 id가 들어있었는데
위에 코드에서 내가 지우고 싶은 todo의 id값을 넣은 todo를 deletetodo의 액션으로 지워준다

그리고 todos.js 에서 리덕스 부분에서 DELETE_TODO 의 케이스가 없었다 그래서 추가했다!



- 상세 페이지에 진입 하였을 때 데이터가 업데이트 되지 않음.

해결 방법 : 
첫번째 문제 useSelector로 가져오고 있는 값이 잘못되었다 
const todo = useSelector((state) => state.todos.todos); 에서
state.todos.todo 로 되어있었다 우린 inital state에서 todos에 값을 저장하고 있기 때문에 
todos.todos로 바꿔줘야한다

두번째 문제 우리가 불러올 값을 이상하게 가져오고 있었기 때문이다
  const foundData = todo.find((item)=> {
    return item.id === params.id || item.id === parseInt(params.id, 10)
  }) 이코드를 사용했다
  todo의 배열에서 id가 parms.id와 일치하는 객체를 찾아 foundData에 값을 넣어주는 코드이다
  그리고 return안에 코드에서 우리 찾는 id, title, body의 값을 foundData로 찾아주면 된다 그럼 문제해결!



- 완료된 카드의 상세 페이지에 진입 하였을 때 올바른 데이터를 불러오지 못함.

해결 방법 : list.jsx 에서 상세페이지로 진입하는 값에 link의 to안에 들어있는 값이
index 였기 때문에 우리가 원하는 카드의 상세페이지에 진입할 수 없었다
그래서 우리가 todos.map을 todo 라는 이름으로 짓고 돌리고 있기 때문에 link안에 to 값을 todo.id를 넣어줘야한다


- 취소 버튼 클릭시 기능이 작동하지 않음.

해결 방법 : Done에 있는 취소버튼이
todo의 id 값을 가져와서 취소를 해야하는데 그냥 함수만 들어있었기 때문이다
={() => onToggleStatusTodo(todo.id)} 이렇게 수정을 했다


- 과제를 마쳤다면 배포도 한번 해볼까요?

네에에~