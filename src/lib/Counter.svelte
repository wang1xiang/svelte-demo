<script lang="ts">
  import { createEventDispatcher } from 'svelte'
  // 父传子
  export let name: string
  export let age: number
  let count: number = 0
  let textValue: string = ''

  const dispatch = createEventDispatcher()
  const increment = () => {
    count += 1
    // 子传父
    const data = 'Hello from Child!'
    dispatch('message', data)
  }

  let doubleCount = `${count * 2}`

  $: doubleCount = `count现在是${count}，翻倍是${doubleCount}`
</script>

<button on:click={increment}>
  count is {count}
  name is {name}, age is {age}
</button>
<input bind:value={textValue} name="books" />
