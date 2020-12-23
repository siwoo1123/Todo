<script>
	import Todo from './Todo.svelte'
	import { writable } from 'svelte/store'

	let title = ''
	let todos = writable([])
	let id = 0

	function createTodo() {
		if (!title.trim() || title == 'ㅤ' || title == '​') {
			return
		}
		$todos.push({
			id,
			title
		})
		$todos = $todos
		title = ''
		id += 1
	}
</script>
<h1 class="textcenter">할일 목록</h1>
<div class="list">
	<input bind:value={title}
		placeholder="원하는 목록 입력"
		type="text"
		style="width: 166.981px; margin: 0 auto;"
		on:keydown={(e) => {e.key === 'Enter' && createTodo()}} />
	<button on:click={createTodo} style="width: 87.216px; margin: 0 auto;">
		추가
	</button>

	<ul>
		{#each $todos as todo}
			<li><Todo todos={todos} {todo} /></li>
		{/each}
	</ul>
</div>

<style>
	.list {
		background-color: #dadada;
		text-align: center;
		border-radius: 50px;
	}
	.textcenter {
		text-align: center;
	}
</style>