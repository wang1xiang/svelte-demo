# Svelte + TS + Vite

## Svelte 语法总结

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

This template should help get you started developing with Svelte and TypeScript in Vite.

## Recommended IDE Setup

[VS Code](https://code.visualstudio.com/) + [Svelte](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode).

## Need an official Svelte framework?

Check out [SvelteKit](https://github.com/sveltejs/kit#readme), which is also powered by Vite. Deploy anywhere with its serverless-first approach and adapt to various platforms, with out of the box support for TypeScript, SCSS, and Less, and easily-added support for mdsvex, GraphQL, PostCSS, Tailwind CSS, and more.

## Technical considerations

**Why use this over SvelteKit?**

- It brings its own routing solution which might not be preferable for some users.
- It is first and foremost a framework that just happens to use Vite under the hood, not a Vite app.

This template contains as little as possible to get started with Vite + TypeScript + Svelte, while taking into account the developer experience with regards to HMR and intellisense. It demonstrates capabilities on par with the other `create-vite` templates and is a good starting point for beginners dipping their toes into a Vite + Svelte project.

Should you later need the extended capabilities and extensibility provided by SvelteKit, the template has been structured similarly to SvelteKit so that it is easy to migrate.

**Why `global.d.ts` instead of `compilerOptions.types` inside `jsconfig.json` or `tsconfig.json`?**

Setting `compilerOptions.types` shuts out all other types not explicitly listed in the configuration. Using triple-slash references keeps the default TypeScript setting of accepting type information from the entire workspace, while also adding `svelte` and `vite/client` type information.

**Why include `.vscode/extensions.json`?**

Other templates indirectly recommend extensions via the README, but this file allows VS Code to prompt the user to install the recommended extension upon opening the project.

**Why enable `allowJs` in the TS template?**

While `allowJs: false` would indeed prevent the use of `.js` files in the project, it does not prevent the use of JavaScript syntax in `.svelte` files. In addition, it would force `checkJs: false`, bringing the worst of both worlds: not being able to guarantee the entire codebase is TypeScript, and also having worse typechecking for the existing JavaScript. In addition, there are valid use cases in which a mixed codebase may be relevant.

**Why is HMR not preserving my local component state?**

HMR state preservation comes with a number of gotchas! It has been disabled by default in both `svelte-hmr` and `@sveltejs/vite-plugin-svelte` due to its often surprising behavior. You can read the details [here](https://github.com/rixo/svelte-hmr#svelte-hmr).

If you have state that's important to retain within a component, consider creating an external store which would not be replaced by HMR.

```ts
// store.ts
// An extremely simple external store
import { writable } from 'svelte/store'
export default writable(0)
```
