---
title: ref
createTime:  2023-5-2
date:  2023/05/02 20:01:27
tags:
  - vue
categories:
  - vue
---

## ref 解析

```ts
  function ref(value) {
    return createRef(value, false);
  }

  function createRef(rawValue, shallow) {
    if (isRef2(rawValue)) {
      return rawValue;
    }
    return new RefImpl(rawValue, shallow);
  }

```

### RefImpl

```ts
  var _a, _b;
  _b = "__v_isRef" /* IS_REF */, _a = "__v_isShallow" /* IS_SHALLOW */;
  var RefImpl = class {
    constructor(value, isShallow2) {
      this.dep = new Dep();
      this[_b] = true;
      this[_a] = false;
      this._rawValue = isShallow2 ? value : toRaw(value);
      this._value = isShallow2 ? value : toReactive(value);
      this["__v_isShallow" /* IS_SHALLOW */] = isShallow2;
    }
    // 获取ref的值
    get value() {
      // 收集依赖
      this.dep.track();
      return this._value;
    }
    set value(newValue) {
      const oldValue = this._rawValue;
      const useDirectValue = this["__v_isShallow" /* IS_SHALLOW */] || isShallow(newValue) || isReadonly(newValue);
      newValue = useDirectValue ? newValue : toRaw(newValue);
      if (hasChanged(newValue, oldValue)) {
        this._rawValue = newValue;
        this._value = useDirectValue ? newValue : toReactive(newValue);
        // 更新依赖，会调用notify 方法实现所有更新
        this.dep.trigger();
      }
    }
  };
```