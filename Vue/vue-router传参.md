# vue-router 传参

```js
this.$router.push({
  name: 'map',
  params: {address}, // 传递 params 时，必须是是已经命名的路由。参数不会显示在地址上，刷新后会丢失
  query: {address}  // 显示在地址上，刷新后不会丢失
})
```

## 传递 params 时

传递 params 时，必须是是已经命名的路由。

```js
this.$router.push({
  name: 'map',
  params: {address}
})
```

参数 params 不会显示在地址上，刷新后会丢失。

```url
http://localhost:8080/#/map
```

## 传递 query 时

可以根据路由的 path 或 name 传递。

```js
this.$router.push({
  name: 'map',
  query: {address}
})
```

```js
this.$router.push({
  path: '/map',
  query: {address}
})
```

参数 query 会显示在地址上，刷新后不会丢失。

```url
http://localhost:8080/#/map?address=XXX
```
