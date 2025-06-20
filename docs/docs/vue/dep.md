---
title: ref
createTime:  2023-5-2
date:  2023/05/02 20:01:27
tags:
  - vue
categories:
  - vue
---

## dep 类

```ts
var Dep = class {
  constructor(computed3) {
    this.computed = computed3;
    this.version = 0;
    /**
     * Link between this dep and the current active effect
     */
    this.activeLink = void 0;
    /**
     * Doubly linked list representing the subscribing effects (tail)
     */
    this.subs = void 0;
    /**
     * For object property deps cleanup
     */
    this.map = void 0;
    this.key = void 0;
    /**
     * Subscriber counter
     */
    this.sc = 0;
    if (true) {
      this.subsHead = void 0;
    }
  }
  // 跟踪依赖收集
  track() {
    /**
     * @desc activeSub 没有活动效果undefined
     * @desc shouldTrack 应该跟踪依赖false
     * @desc activeSub === this.computed 活动效果是否为当前计算属性
     */
    if (!activeSub || !shouldTrack || activeSub === this.computed) {
      return;
    }
    let link = this.activeLink;
    if (link === void 0 || link.sub !== activeSub) {
      link = this.activeLink = new Link(activeSub, this);
      if (!activeSub.deps) {
        activeSub.deps = activeSub.depsTail = link;
      } else {
        link.prevDep = activeSub.depsTail;
        activeSub.depsTail.nextDep = link;
        activeSub.depsTail = link;
      }
      addSub(link);
    } else if (link.version === -1) {
      link.version = this.version;
      if (link.nextDep) {
        const next = link.nextDep;
        next.prevDep = link.prevDep;
        if (link.prevDep) {
          link.prevDep.nextDep = next;
        }
        link.prevDep = activeSub.depsTail;
        link.nextDep = void 0;
        activeSub.depsTail.nextDep = link;
        activeSub.depsTail = link;
        if (activeSub.deps === link) {
          activeSub.deps = next;
        }
      }
    }
    return link;
  }
  // 触发依赖更新
  trigger() {
    this.version++;
    globalVersion++;
    this.notify();
  }
  // 通知所有订阅依赖效果更新
  notify() {
    startBatch();
    try {
      
      for (let link = this.subs; link; link = link.prevSub) {
        if (link.sub.notify()) {
          
          link.sub.dep.notify();
        }
      }
    } finally {
      endBatch();
    }
  }
};
```

## Link 类

```ts
export class Link {
  /**
   * - Before each effect run, all previous dep links' version are reset to -1
   * - During the run, a link's version is synced with the source dep on access
   * - After the run, links with version -1 (that were never used) are cleaned
   *   up
   */
  version: number

  /**
   * Pointers for doubly-linked lists
   */
  nextDep?: Link
  prevDep?: Link
  nextSub?: Link
  prevSub?: Link
  prevActiveLink?: Link

  constructor(
    public sub: Subscriber,
    public dep: Dep,
  ) {
    this.version = dep.version
    this.nextDep =
      this.prevDep =
      this.nextSub =
      this.prevSub =
      this.prevActiveLink =
        undefined
  }
}
```