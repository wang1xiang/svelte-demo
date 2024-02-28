### 变量

定义变量时，不需要像 vue 那样使用 ref，也不需要像 react 那样使用 useState。只需要**直接命名变量**即可，这就是一个响应式的变量了

### 事件

事件需要用到 Svelte 的**语法 on**:，比如点击事件 `on:click={xxxxx}`

### 父传子

遵循单项数据流

Svelte 提供了 `export` 关键字，子组件中可以使用 `export` 来接收，结合 typescript 去定义属性的类型

```ts
<script lang="ts">
  export let name: string;
  export let age: number;
</script>

<div>我叫{name}，今年{age}岁</div>
```

父组件中，Svelte 中提供了 `{}` 这样的语法糖，去支持父组件传值到子组件中

### 子传父

- 子组件：使用 `createEventDispatcher` 派发到父组件

  ```ts
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  ...
  dispatch('message', 'hello');
  ```

- 父组件：使用 `on:message` 接收子组件传过来的

  ```ts
  <Counter {name} {age}  on:message={handleMessage}  />
  ```

### 双向绑定

语法糖 `bind:value`

### 插槽

提供插槽 `slot`，并且支持默认插槽和具名插槽，与 Vue 一致

### 生命周期

onMount: 组件挂载
beforeUpdate: 组件更新之前
afterUpdate: 组件更新之后
onDestroy: 组件销毁

### watch & computed

提供 `$` 语法糖

```js
let doubleCount = `${count * 2}`

$: count = `count现在是${count}`
```

### 条件渲染

```js
{#if age > 50}
  <p>老年人</p>
{:else if count > 30}
  <p>中年人</p>
{:else}
  <p>小朋友</p>
{/if}
```

### 循环渲染

```js
{#each items as item (item.id)}
  <p>{item.name}</p>
{/each}
```
