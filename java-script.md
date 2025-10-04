# 📘 JavaScript & Problem Solving – 50 Interview Questions & Answers

This document contains **50 JavaScript & problem-solving interview questions with answers**, tailored for Vishal’s profile (6+ years experience, full-stack background, real-world use cases in Healthcare, E‑Commerce, and Authentication). Algorithm answers include **time/space complexity** and clean JS implementations.

---

## 1. Explain the Event Loop in JavaScript.
**Answer:** JavaScript is single-threaded but async work is coordinated by the **event loop**. The call stack runs sync code; async tasks (timers, I/O, fetch) resolve in Web APIs, enqueue callbacks into **task/microtask queues** (microtasks = promises, mutation observers). The event loop pushes microtasks before tasks when the stack is empty, enabling deterministic promise ordering.

---

## 2. What are closures? Give a real-world example.
**Answer:** A closure is a function that **captures variables from its lexical scope** even after the outer function returns.
```js
function makeCounter() {
  let count = 0;               // captured
  return () => ++count;
}
const counter = makeCounter();
counter(); // 1
```
*Use case:* Preserving component-local utilities (e.g., debounced search handler) without leaking globals.

---

## 3. Difference between `var`, `let`, `const`.
**Answer:** `var` is function-scoped & hoisted (re-declarable). `let`/`const` are block-scoped; `const` prevents re-assignment (not deep immutability). Avoid `var` in modern code.

---

## 4. Explain hoisting in JavaScript.
**Answer:** Declarations are moved to the top of their scope. `var` is hoisted with value `undefined`; `let`/`const` are hoisted but **temporal dead zone (TDZ)** applies until initialization. Function declarations are hoisted with definitions.

---

## 5. Deep vs shallow copy.
**Answer:** Shallow copy copies top-level references; deep copy recursively clones.
```js
const shallow = {...obj};
const deep = structuredClone(obj); // or JSON.parse(JSON.stringify(obj)) with caveats
```
*Caveats:* Dates, Maps/Sets, functions aren’t preserved by JSON method.

---

## 6. `this` in arrow vs normal functions.
**Answer:** Arrow functions **lexically bind** `this`; normal functions’ `this` depends on call-site (`call/apply/bind`, method, or default/global).

---

## 7. Implement debouncing.
```js
function debounce(fn, delay){
  let t; return (...args)=>{ clearTimeout(t); t=setTimeout(()=>fn(...args), delay); };
}
```
*Use:* Search inputs to limit API calls.

---

## 8. Implement throttling.
```js
function throttle(fn, delay){
  let last=0; return (...a)=>{ const now=Date.now(); if(now-last>=delay){ last=now; fn(...a);} };
}
```

---

## 9. Prototypal inheritance.
**Answer:** Objects inherit via the `[[Prototype]]` chain. Methods shared via prototype reduce per-instance memory.

---

## 10. `==` vs `===`.
**Answer:** `===` strict (no coercion). Prefer `===` to avoid coercion pitfalls.

---

## 11. Currying.
```js
const add = a=>b=>c=>a+b+c; add(1)(2)(3);
```
*Use:* Partially apply config for formatters/validators.

---

## 12. Polyfill `Array.map`.
```js
Array.prototype.myMap=function(cb,thisArg){
  const out=[]; for(let i=0;i<this.length;i++) if(i in this) out.push(cb.call(thisArg,this[i],i,this));
  return out;
};
```

---

## 13. Polyfill `Promise.all`.
```js
Promise.myAll = (arr)=> new Promise((res,rej)=>{
  const n=arr.length, out=new Array(n); let done=0;
  if(n===0) return res([]);
  arr.forEach((p,i)=>Promise.resolve(p).then(v=>{ out[i]=v; if(++done===n) res(out); }).catch(rej));
});
```

---

## 14. Async/await with error handling.
```js
async function fetchJSON(url){
  try{ const r=await fetch(url); if(!r.ok) throw new Error(r.status); return r.json(); }
  catch(e){ /* log/telemetry */ throw e; }
}
```

---

## 15. Promise chaining example.
```js
fetch('/api1').then(r=>r.json())
  .then(d1=>fetch('/api2?id='+d1.id))
  .then(r=>r.json()).catch(console.error);
```

---

## 16. `call`, `apply`, `bind`.
**Answer:** `call(a, ...args)`, `apply(a, argsArray)`, `bind(a)` returns a new function with bound `this`.

---

## 17. Detect memory leaks.
**Answer:** DevTools **Performance/Memory**; watch for detached DOM nodes, unremoved listeners, growing arrays/singletons.

---

## 18. Event delegation.
**Answer:** Attach one listener on a parent; use `event.target`/`matches` to handle children efficiently.

---

## 19. Service workers.
**Answer:** Proxy network requests for offline/PWA, background sync, push notifications. Must be HTTPS and scope-bound.

---

## 20. Reverse a linked list.
```js
function reverse(head){ let prev=null,c=head; while(c){ const n=c.next; c.next=prev; prev=c; c=n;} return prev; }
// Time O(n), Space O(1)
```

---

## 21. Longest substring without repeating characters.
```js
function lengthOfLongestSubstring(s){
  const idx=new Map(); let left=0,max=0;
  for(let r=0;r<s.length;r++){
    if(idx.has(s[r]) && idx.get(s[r])>=left) left=idx.get(s[r])+1;
    idx.set(s[r],r); max=Math.max(max,r-left+1);
  } return max;
}
// Time O(n), Space O(k)
```

---

## 22. Design an LRU cache.
```js
class LRU{
  constructor(cap){ this.cap=cap; this.map=new Map(); }
  get(k){ if(!this.map.has(k)) return -1; const v=this.map.get(k); this.map.delete(k); this.map.set(k,v); return v; }
  set(k,v){ if(this.map.has(k)) this.map.delete(k); this.map.set(k,v); if(this.map.size>this.cap){ const fk=this.map.keys().next().value; this.map.delete(fk);} }
}
// Ops O(1) average
```

---

## 23. Generators.
**Answer:** Functions that can pause/resume with `yield`; useful for iterables, pipelines, or cooperative async flows.
```js
function* idGen(){ let i=0; while(true) yield ++i; }
```

---

## 24. WeakMap vs Map (and WeakSet vs Set).
**Answer:** WeakMap/WeakSet hold **weak references** to keys (must be objects); allow garbage collection; non-iterable. Good for private metadata.

---

## 25. Flatten a nested array.
```js
const flat = (arr)=> arr.flat(Infinity);
// Manual DFS
function flatDFS(a){ const out=[]; (function go(x){ for(const v of x) Array.isArray(v)?go(v):out.push(v); })(a); return out; }
// Time O(n), Space O(n)
```

---

## 26. Debounce API calls with immediate option.
```js
function debounceImmediate(fn, delay){
  let t, called=false; return (...a)=>{
    if(!t){ fn(...a); called=true; }
    clearTimeout(t); t=setTimeout(()=>{ t=null; called=false; }, delay);
  };
}
```

---

## 27. Temporal Dead Zone (TDZ).
**Answer:** Accessing `let`/`const` before initialization throws ReferenceError. Encourages predictable initialization order.

---

## 28. Deep clone patterns.
```js
const deep1 = structuredClone(obj);
const deep2 = JSON.parse(JSON.stringify(obj)); // beware Date/Map/Set/NaN/Infinity
```

---

## 29. Optional chaining & nullish coalescing.
```js
const name = user?.profile?.name ?? 'Guest';
```

---

## 30. Merge two sorted arrays.
```js
function merge(a,b){ const out=[]; let i=0,j=0; while(i<a.length&&j<b.length){ out.push(a[i]<=b[j]?a[i++]:b[j++]); } return out.concat(a.slice(i),b.slice(j)); }
// Time O(n+m), Space O(n+m)
```

---

## 31. Find the missing number (1..n).
```js
function missing(nums){ const n=nums.length+1; const sum=n*(n+1)/2; return sum-nums.reduce((a,b)=>a+b,0); }
// Time O(n), Space O(1)
```

---

## 32. Check palindrome (alphanumeric, case-insensitive).
```js
function isPal(s){ s=s.toLowerCase().replace(/[^a-z0-9]/g,''); let l=0,r=s.length-1; while(l<r) if(s[l++]!==s[r--]) return false; return true; }
// O(n)
```

---

## 33. Word frequency counter.
```js
function freq(s){ const map=Object.create(null); for(const w of s.toLowerCase().match(/\b\w+\b/g)||[]) map[w]=(map[w]||0)+1; return map; }
// O(n)
```

---

## 34. Binary search.
```js
function bsearch(a,x){ let l=0,r=a.length-1; while(l<=r){ const m=(l+r>>1); if(a[m]===x) return m; a[m]<x? l=m+1: r=m-1; } return -1; }
// O(log n)
```

---

## 35. Big‑O quick guide.
**Answer:** Array push O(1), unshift O(n); object prop access O(1); Map/Set ops O(1) avg; sort O(n log n).

---

## 36. Two Sum.
```js
function twoSum(a,t){ const m=new Map(); for(let i=0;i<a.length;i++){ const need=t-a[i]; if(m.has(need)) return [m.get(need), i]; m.set(a[i], i); } }
// O(n)
```

---

## 37. Sliding window pattern.
**Answer:** Maintain a moving window with two pointers; expand to satisfy condition, shrink to maintain constraint (e.g., longest substring, min window).

---

## 38. Maximum subarray sum (Kadane).
```js
function maxSub(a){ let best=a[0], cur=a[0]; for(let i=1;i<a.length;i++){ cur=Math.max(a[i],cur+a[i]); best=Math.max(best,cur);} return best; }
// O(n)
```

---

## 39. Sync vs async JS.
**Answer:** Sync blocks the call stack; async uses callbacks/promises/await to defer work without blocking. I/O is delegated to the environment.

---

## 40. How does `setTimeout` work under the hood?
**Answer:** Timer registers with Web APIs; after delay, callback enqueued in **task queue**; executed when stack is empty and microtasks are drained.

---

## 41. Implement memoization.
```js
function memo(fn){ const cache=new Map(); return (...a)=>{ const k=JSON.stringify(a); if(cache.has(k)) return cache.get(k); const v=fn(...a); cache.set(k,v); return v; } }
```

---

## 42. Pure functions & immutability.
**Answer:** Pure = same inputs → same output, no side effects. Immutability avoids accidental mutations; use spreads, `Object.freeze` (shallow), immutable data libs if needed.

---

## 43. Implement a stack.
```js
class Stack{ constructor(){this.a=[];} push(x){this.a.push(x);} pop(){return this.a.pop();} peek(){return this.a.at(-1);} }
```

---

## 44. Queue using two stacks.
```js
class Queue{ constructor(){ this.in=[]; this.out=[]; }
  enqueue(x){ this.in.push(x); }
  dequeue(){ if(!this.out.length) while(this.in.length) this.out.push(this.in.pop()); return this.out.pop(); }
}
// Amortized O(1)
```

---

## 45. Recursion basics.
**Answer:** A function that calls itself with smaller input; ensure **base case** and **progress** to avoid infinite loops/stack overflow.

---

## 46. Fibonacci with DP.
```js
function fib(n){ if(n<2) return n; const dp=[0,1]; for(let i=2;i<=n;i++) dp[i]=dp[i-1]+dp[i-2]; return dp[n]; }
// O(n) time, O(n) space (or O(1) rolling)
```

---

## 47. Event bubbling vs capturing.
**Answer:** Capturing: document→target; Bubbling: target→document. Use `{capture:true}` to listen on capture; `stopPropagation()` to halt.

---

## 48. Merge sort.
```js
function mergeSort(a){ if(a.length<2) return a; const m=a.length>>1; return merge(mergeSort(a.slice(0,m)), mergeSort(a.slice(m)));
}
// O(n log n) time, O(n) space
```

---

## 49. Generate balanced parentheses.
```js
function gen(n){ const out=[]; (function backtrack(s=",", open=0, close=0){ if(s.length===2*n){ out.push(s); return; } if(open<n) backtrack(s+'(',open+1,close); if(close<open) backtrack(s+')',open,close+1); })('' ,0,0); return out; }
// O(Catalan(n))
```

---

## 50. Top K frequent elements.
```js
function topK(nums,k){ const m=new Map(); nums.forEach(x=>m.set(x,(m.get(x)||0)+1));
  const buckets=Array(nums.length+1).fill(0).map(()=>[]);
  for(const [val,f] of m) buckets[f].push(val);
  const out=[]; for(let f=buckets.length-1; f>=0 && out.length<k; f--) out.push(...buckets[f]);
  return out.slice(0,k);
}
// O(n)
```

---

### Bonus Design/JS Pragmatics (quick answers)
- **Min window substring (idea):** Expand right to include all chars, shrink left to minimal; O(n).
- **Find cycle in linked list:** Floyd’s tortoise-hare; O(n), O(1).
- **Quickselect (kth):** Average O(n) using partition.
- **Floating point pitfall:** `0.1+0.2!==0.3` due to binary representation; compare with epsilon.
- **`Promise.any` vs `allSettled` vs `race`:** `any` resolves first fulfilled, `race` first settled, `allSettled` waits for all.
- **JSON stringify limits:** Drops functions/undefined, loses Map/Set/Date info.
- **Map vs Object:** Map maintains insertion order, any keys, better perf for large dynamic key sets.

---

✅ Completed **50 JavaScript & Problem‑Solving Q&A** with runnable snippets and complexities.
