<script>
  let statusList = [
	{status: 1, name: "未着手"},
	{status: 2, name: "着手"},
	{status: 3, name: "完了"},
  ];
  let todoInput = "";
  let todoList = [];
  let selected;
  let deleteTodo = function(i){
	todoList.splice(i, 1);
	todoList = JSON.parse(JSON.stringify(todoList));
  }
  let click = function(){
	if(selected && (todoInput.length >= 1)){
	  todoList = [
		{name: todoInput, status: selected},
		...todoList,
	  ];
	  todoInput = "";
	}else{
	  alert("selected or todoInput is empty.");
	}
  }
</script>

<main>
  <h2>Svelte ToDo</h2>
  <div>
	<input type="text" bind:value={todoInput} />
	<select bind:value={selected}>
	  {#each statusList as status, i}
		<option value={status}>{status.name}</option>
	  {/each}
	</select>
	<button on:click={click}>submit</button>
  </div>

  {#each statusList.map(x => x) as st}
	<h3>{st.name}</h3>
	<ul>
		{#each todoList.filter(x => x.status.status == st.status) as todo, i}
		  <li>
			<input type="text" bind:value={todo.name}/>
			:
			<select bind:value={todo.status}>
			  {#each statusList as status, i}
				<option value={status}>{status.name}</option>
			  {/each}
			</select>
			<button on:click={() => deleteTodo(i)}>削除</button>
		  </li>
		{/each}
	  </ul>
  {/each}
</main>
