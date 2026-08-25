# Express Async Error Handling

In Express 4, async route handlers that reject don't reach error middleware by default. Wrap them with this helper:

```js
const asyncHandler = fn => (req, res, next) =>
  Promise.resolve(fn(req, res, next)).catch(next);
```

Usage:

```js
app.get('/user', asyncHandler(async (req, res) => {
  const user = await db.findUser(req.params.id);
  res.json(user);
}));
```

Express 5 handles promise rejections automatically, but this pattern is still useful for existing Express 4 projects.
