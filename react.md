# 📘 Core Frontend (React + Next.js) – 50 Interview Questions & Answers

This document contains **50 advanced React.js & Next.js interview questions with detailed answers**, tailored for Vishal’s profile (6+ years experience, Module Lead at Happiest Minds, strong in React/Next.js, Auth, Razorpay, FHIR APIs).

---

## 1. Explain React Fiber architecture.
**Answer:** React Fiber is a rewrite of React’s reconciliation algorithm. It splits rendering into units called **fibers**, allowing React to pause, prioritize, or resume work. This enables **concurrent rendering**, smooth animations, and better handling of large updates.

---

## 2. How does React reconcile changes in the Virtual DOM?
**Answer:** React compares the Virtual DOM tree with the previous one using the **diffing algorithm**. It uses **keys** for list items to track changes and updates only the necessary DOM nodes, improving performance.

---

## 3. Difference between `useEffect`, `useLayoutEffect`, and `useInsertionEffect`.
**Answer:**
- `useEffect`: Runs asynchronously after paint → used for API calls, subscriptions.
- `useLayoutEffect`: Runs synchronously before paint → good for DOM measurements.
- `useInsertionEffect`: Runs before mutations → useful for CSS-in-JS libraries.

---

## 4. What are Suspense and Concurrent features in React?
**Answer:**
- **Suspense:** Allows components to wait for async data before rendering.
- **Concurrent Mode:** Enables React to render in chunks, pause/resume, leading to smoother UI.

---

## 5. How would you optimize re-rendering in a large React app?
**Answer:**
- Use `React.memo`, `useMemo`, `useCallback`.
- Split components.
- Use virtualization (e.g., react-window).
- Avoid unnecessary context re-renders.
- Optimize dependency arrays in hooks.

---

## 6. Context API vs Redux Toolkit.
**Answer:**
- **Context API:** Simple state sharing, but triggers re-renders.
- **Redux Toolkit:** Scalable, structured, middleware support, devtools. Best for enterprise apps.

---

## 7. What is the difference between SSR and SSG in Next.js?
**Answer:**
- **SSR:** Page generated on each request.
- **SSG:** Page generated at build time.
- *Use Case:* Doctor availability page → SSR, Magazine subscription page → SSG.

---

## 8. What is Incremental Static Regeneration (ISR) in Next.js?
**Answer:** ISR allows re-generation of static pages at runtime with `revalidate`, enabling fresh data without full rebuilds.

---

## 9. How does App Router differ from Pages Router in Next.js?
**Answer:**
- **App Router:** Uses `app/`, supports layouts, React Server Components, streaming.
- **Pages Router:** Legacy, `pages/` directory, less flexible.

---

## 10. How would you implement authentication in Next.js?
**Answer:**
- API routes + JWT/Auth0/Cognito.
- Secure cookies for tokens.
- Middleware for route protection.

---

## 11. What is the role of middleware in Next.js?
**Answer:** Middleware runs before requests resolve, used for **auth checks, logging, security, redirects**.

---

## 12. How would you handle API caching in Next.js?
**Answer:**
- ISR (`revalidate`).
- HTTP caching (`Cache-Control`).
- SWR or React Query.
- Redis for backend caching.

---

## 13. Difference between `getServerSideProps`, `getStaticProps`, and `getInitialProps`.
**Answer:**
- `getServerSideProps`: Runs on every request.
- `getStaticProps`: Runs at build time.
- `getInitialProps`: Legacy, runs on client + server.

---

## 14. How to handle SEO in Next.js?
**Answer:**
- `next/head` for meta.
- SSR/SSG for crawlers.
- Structured schema.
- Fast performance.

---

## 15. How would you lazy load components in React?
**Answer:** Use `React.lazy` with `Suspense`. Reduces initial bundle size.

---

## 16. Explain Error Boundaries in React.
**Answer:** Components that catch errors in child components, using `componentDidCatch`. Show fallback UI instead of breaking the app.

---

## 17. How would you integrate Razorpay in a Next.js application?
**Answer:**
- Backend API route creates order.
- Frontend loads Razorpay checkout.
- Backend verifies signature.

---

## 18. How do you implement dynamic routing in Next.js?
**Answer:**
- Use `[param].js` for dynamic routes.
- Use `getStaticPaths` for pre-rendering dynamic pages.

---

## 19. Difference between `useState` and `useReducer`.
**Answer:**
- `useState`: Simple local state.
- `useReducer`: Complex state transitions, centralized logic.

---

## 20. How do you secure API routes in Next.js?
**Answer:**
- Middleware auth.
- Validate JWTs.
- Role-based checks.

---

## 21. What are rules of React hooks?
**Answer:**
- Call hooks only at top level.
- Call hooks only inside React functions.

---

## 22. How would you manage global state across a large app?
**Answer:**
- Redux Toolkit.
- Zustand, Jotai for lightweight.
- Context for small cases.

---

## 23. Explain Suspense for data fetching.
**Answer:** Lets components suspend rendering until data resolves. Often paired with React Query or Relay.

---

## 24. How do you handle internationalization (i18n) in Next.js?
**Answer:**
- Built-in i18n routing in Next.js config.
- `next-translate` library.

---

## 25. Explain Hydration in Next.js.
**Answer:** Process where React takes over server-rendered HTML and makes it interactive on the client.

---

## 26. Difference between CSR, SSR, and SSG.
**Answer:**
- CSR: Rendering in browser.
- SSR: Server-side at request.
- SSG: Static build-time pages.

---

## 27. How to implement image optimization in Next.js?
**Answer:** Use `next/image`. Provides lazy loading, resizing, and format conversion.

---

## 28. What is the purpose of `next/head`?
**Answer:** For managing meta tags, SEO, and OpenGraph tags.

---

## 29. How would you integrate FHIR APIs into a Next.js app?
**Answer:**
- Fetch data in `getServerSideProps`.
- Parse JSON FHIR resources.
- Display structured medical data.

---

## 30. Explain React Portal.
**Answer:** Allows rendering child components outside parent DOM hierarchy (e.g., modals, tooltips).

---

## 31. What is code splitting in React/Next.js?
**Answer:** Breaking code into smaller bundles loaded on demand. Achieved with dynamic import or lazy.

---

## 32. How to handle authentication tokens in Next.js?
**Answer:**
- Store in HttpOnly cookies.
- Use API routes for refreshing.

---

## 33. What is React Profiler?
**Answer:** A devtool to measure rendering performance, helps detect slow components.

---

## 34. How to secure sensitive env variables in Next.js?
**Answer:**
- Store in `.env.local`.
- Access via `process.env` in server-side only.

---

## 35. What are React keys? Why are they important?
**Answer:** Keys identify list items uniquely, helping React track changes efficiently.

---

## 36. How to debug performance issues in React?
**Answer:**
- React Profiler.
- Chrome Performance tab.
- Lighthouse audits.

---

## 37. Explain React Suspense boundaries.
**Answer:** Boundaries define fallback UI for child components that are waiting for data.

---

## 38. How do you handle forms with validation in React?
**Answer:**
- React Hook Form (lightweight).
- Yup for validation.
- Custom hooks.

---

## 39. Compare Formik vs React Hook Form.
**Answer:**
- Formik: More features, heavier.
- RHF: Lightweight, performant.

---

## 40. How to persist Redux state across refreshes?
**Answer:**
- `redux-persist` library.
- Store in localStorage/sessionStorage.

---

## 41. How to structure a large React project?
**Answer:**
- Feature-based foldering.
- Separate UI library, hooks, services.
- Use aliases for imports.

---

## 42. Explain API routes in Next.js.
**Answer:** API routes live in `pages/api/`. Good for lightweight serverless backend logic.

---

## 43. What are dynamic imports in Next.js?
**Answer:** Import modules/components lazily using `next/dynamic`.

---

## 44. How to manage role-based access in React?
**Answer:**
- Store user role in state.
- Conditional rendering.
- Middleware checks for protected routes.

---

## 45. Difference between shallow vs deep rendering in testing.
**Answer:**
- Shallow: Only renders one component (ignores children).
- Deep: Renders with all children.

---

## 46. How to implement breadcrumbs in Next.js?
**Answer:**
- Extract route segments.
- Map to user-friendly names.
- Render as links.

---

## 47. What is React Strict Mode?
**Answer:** A dev-only feature that highlights potential problems like unsafe lifecycles and double-invokes effects.

---

## 48. How would you implement dark mode in Next.js?
**Answer:**
- Store preference in localStorage.
- Use CSS variables or Tailwind dark mode.
- Hydrate on app load.

---

## 49. How did you integrate adaptive notifications in projects?
**Answer:**
- Used Webex Adaptive Cards API.
- Notifications triggered by backend events.
- Handled scheduled + real-time delivery.

---

## 50. What is React Server Component (RSC)?
**Answer:** New feature in React + Next.js App Router. Components render on the server, reducing bundle size and improving performance.

---

