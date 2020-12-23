<script>
    export let todos
    export let todo

    let title = ''
    let gon = ' '
    let isEdit = false

    function onEdit() {
        isEdit = true
        title = todo.title
    }
    function offEdit() {
        isEdit = false
    }
    function updateTodo() {
        todo.title = title
        offEdit()
    }
    function deleteTodo() {
        $todos = $todos.filter(t => t.id !== todo.id)
        console.log(todos)
    }
</script>


{#if isEdit}
    <div>
        <input type="text"
            bind:value={title}
            on:keydown={(e) => {e.key === 'Enter' && updateTodo()}} />
        <button on:click={updateTodo}>
            제출
        </button>
        <button on:click={offEdit}>
            취소
        </button>
    </div>
{:else}
    <div>
        <input type="checkbox" id="check">{gon}{gon}<label for="check">{todo.id + 1}. {todo.title}</label>
        <button on:click={onEdit}>
            수정
        </button>
        <button on:click={deleteTodo}>
            삭제
        </button>
    </div>
{/if}
<style>
    label {
		display: inline;
	}
</style>
