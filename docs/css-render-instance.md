# `CssRender` Instance
`CssRender` instance can be created by the following codes:
```js
import CssRender from 'css-render'

const config = {
  // ... 
}
const cssr = CssRender(config) // cssr is a CssRender instance
```
## Config
```typescript
interface Config {
  // whether to render the CSS of a CNode with empty properties (eg. {})
  // default is false
  keepEmptyBlock: boolean
}
```
## Properties on the Instance
the instance(`cssr`) has some public properties:
- `c(...)`: the method to create a `CNode`, see [Create a CNode & Render a CNode Tree](cnode-and-render.md).
- `context`: the context of the instance, default is `{}`. It may be used by a plugin or in the rendering phase of a `CNode` tree.
- `use(plugin)`: bind the instance with a plugin.
