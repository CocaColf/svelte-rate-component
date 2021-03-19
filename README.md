# svelte Rate component

This is a Rate component implementation with [Svelte](https://svelte.dev).

![demo image]('./svelte_rate.gif')

## How to run

```bash
yarn install
yarn dev
```
## Props

| Name | Description | Type  | Default |
| --- | --- | --- | --- |
| `modelValue` | Score | `string \| number` | 0 | 
| `strokeColor` | Color of highlight | `string` | `#f7ba2a` | 
| `backgroundColor` | Color of not selected | `string` | `#c6d1de` | 
| `count` | Number  of icon | `string \| number` | 5 | - | - | 
| `icon` | Iconfont name | `string` | `icon-favorite-filling` | 
| `allowHalf` | Support half points | `boolean` | false |
| `disabled` | Readonly | `boolean` | false |
| `tooltips` | Suspension prompt for each element | `Array` | [] |
| `allowClear` | Clear all when click slected icon | `boolean` | false |

## event

| Name | Description | Type of value |
| --- | --- | --- |
| `change` | Score change | `number` |
