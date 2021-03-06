# Advanced Mount & Unmount Options
Every [CNode](https://github.com/07akioni/css-render/blob/master/docs/overview.md) has `mount` & `unmount` methods.

They can help you mount style to the HTML document.

> Since `CNode` support lazy selector, properties and children evaluation, and some call of the `mount` will render the `CNode` again, the mounted style can be different in different mount.

## Mount
Render the `CNode`'s style and mount it to document.

```typescript
type mount = (
  options?: {
    target?: string | number | HTMLStyleElement | null, 
    props?: any,
    count?: boolean
  }
) => HTMLStyleElement | null
```

### `target`
- If `target` or `options` is `undefined`, every call of mount method will create a new `style` element with rendered style and mount it `document.head`.
- If `target` is a `string` or `number`. It will mount the style on a `style[cssr-id="${target}"]` element to `document.head` and set `mount-count` attribute of the element to `1`. For example: `<head><style cssr-id="target" mount-count="1">...</style></head>`. If the element already exists, the `mount` method will **not** refresh the content of the element but plus the `mount-count` attribute of the element by `1`.
- If `target` is a `HTMLStyleElement`, and the `target` has no `mount-count` attribute, the `innerHTML` of the `target` will be set to the rendered style and the `mount-count` attribute will be set to `1`, or it will only plus the `mount-count` attribute of the `target` by `1` and not refresh the target's content.
- If `target` is `null`, it will do nothing.
### `props`
The `props` will be used as the render function's `props` during this mount.
### `count`
- If `count` is not set, it will be treated as `true`.
- If it is set to `false`, the mount won't have any effects on `mount-count` of the target.
### Return Value
The target element for the style to mount on.


## Unmount
Unmount the style of the CNode.

```typescript
type unmount = (
  options?: {
    target?: string | number | HTMLStyleElement | null,
    count?: boolean
  }
) : void
```

### `target`
- If `target` or `options` is `undefined`, every mounted elements of the `CNode` will be unmounted.
- If `target` is a `string` or `number`. It will unmount `style[cssr-id="${target}"]` element mounted by the `CNode` if the element's `mount-count` is `1` or `null`. Or it will minus the element's `mount-count` by `1`.
- If `target` is a `HTMLStyleElement`. It will clear the `innerHTML` of the element when its `mount-count` is `1` or `null`. Or it will minus the element's `mount-count` by `1`.
- If `target` is `null`, it will do nothing.

### `count`
- If `count` is not set, it will be treated as `true`.
- If `count` is set to `false`, it will unmount the style regardless of `mount-count` attribute of the target.

---

## Note
If you are dynamically mounting & unmounting styles, manage the `target` carefully.
