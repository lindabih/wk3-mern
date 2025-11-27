# wk3-mern
week3 Mern

diff --git a/tailwind.config.cjs b/tailwind.config.cjs
new file mode 100644
index 0000000..1111111
--- /dev/null
+++ b/tailwind.config.cjs
@@ -0,0 +1,12 @@
+module.exports = {
+  content: [
+    "./index.html",
+    "./src/**/*.{js,jsx,ts,tsx}"
+  ],
+  darkMode: 'class',
+  theme: { extend: {} },
+  plugins: [],
+}
+
+
+diff --git a/postcss.config.cjs b/postcss.config.cjs
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/postcss.config.cjs
+@@ -0,0 +1,9 @@
+ module.exports = {
+   plugins: {
+     tailwindcss: {},
+     autoprefixer: {},
+   },
+ }
+
+diff --git a/src/index.css b/src/index.css
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/index.css
+@@ -0,0 +1,8 @@
+ @tailwind base;
+ @tailwind components;
+ @tailwind utilities;
+
+ /* small helper animation */
+ .fade { transition: all 150ms ease; }
+
+diff --git a/src/main.jsx b/src/main.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/main.jsx
+@@ -0,0 +1,23 @@
+import React from 'react'
+import { createRoot } from 'react-dom/client'
+import { BrowserRouter } from 'react-router-dom'
+import App from './App'
+import './index.css'
+import { ThemeProvider } from './context/ThemeContext'
+
+createRoot(document.getElementById('root')).render(
+  <React.StrictMode>
+    <ThemeProvider>
+      <BrowserRouter>
+        <App />
+      </BrowserRouter>
+    </ThemeProvider>
+  </React.StrictMode>
+)
+
+diff --git a/src/App.jsx b/src/App.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/App.jsx
+@@ -0,0 +1,20 @@
+import React from 'react'
+import { Routes, Route } from 'react-router-dom'
+import Home from './pages/Home'
+import TasksPage from './pages/TasksPage'
+import PostsPage from './pages/PostsPage'
+import Layout from './components/Layout'
+
+export default function App(){
+  return (
+    <Layout>
+      <Routes>
+        <Route path="/" element={<Home />} />
+        <Route path="/tasks" element={<TasksPage />} />
+        <Route path="/posts" element={<PostsPage />} />
+      </Routes>
+    </Layout>
+  )
+}
+
+diff --git a/src/context/ThemeContext.jsx b/src/context/ThemeContext.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/context/ThemeContext.jsx
+@@ -0,0 +1,32 @@
+import React, { createContext, useContext, useEffect, useState } from 'react'
+
+const ThemeContext = createContext()
+
+export const ThemeProvider = ({ children }) => {
+  const [theme, setTheme] = useState(() => localStorage.getItem('theme') || 'light')
+
+  useEffect(() => {
+    const root = document.documentElement
+    if (theme === 'dark') root.classList.add('dark')
+    else root.classList.remove('dark')
+    localStorage.setItem('theme', theme)
+  }, [theme])
+
+  const toggle = () => setTheme(t => (t === 'light' ? 'dark' : 'light'))
+
+  return <ThemeContext.Provider value={{ theme, toggle }}>{children}</ThemeContext.Provider>
+}
+
+export const useTheme = () => useContext(ThemeContext)
+
+diff --git a/src/components/Button.jsx b/src/components/Button.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/components/Button.jsx
+@@ -0,0 +1,22 @@
+import React from 'react'
+
+export default function Button({ children, variant = 'primary', ...props }){
+  const base = "px-4 py-2 rounded-md font-medium focus:outline-none fade"
+  const map = {
+    primary: "bg-blue-600 text-white hover:bg-blue-700 dark:bg-blue-500 dark:hover:bg-blue-600",
+    secondary: "bg-gray-200 text-gray-800 hover:bg-gray-300 dark:bg-gray-700 dark:text-gray-200",
+    danger: "bg-red-600 text-white hover:bg-red-700 dark:bg-red-500",
+  }
+  return <button className={`${base} ${map[variant]}`} {...props}>{children}</button>
+}
+
+diff --git a/src/components/Card.jsx b/src/components/Card.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/components/Card.jsx
+@@ -0,0 +1,10 @@
+import React from 'react'
+
+export default function Card({ children, className = '' }){
+  return (
+    <div className={`bg-white dark:bg-gray-800 shadow rounded-lg p-4 ${className}`}>
+      {children}
+    </div>
+  )
+}
+
+diff --git a/src/components/Navbar.jsx b/src/components/Navbar.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/components/Navbar.jsx
+@@ -0,0 +1,25 @@
+import React from 'react'
+import { Link } from 'react-router-dom'
+import { useTheme } from '../context/ThemeContext'
+import Button from './Button'
+
+export default function Navbar(){
+  const { theme, toggle } = useTheme()
+  return (
+    <nav className="bg-white dark:bg-gray-900 border-b dark:border-gray-700">
+      <div className="max-w-6xl mx-auto flex items-center justify-between p-4">
+        <div className="flex items-center gap-4">
+          <Link to="/" className="text-xl font-bold">Week3 React</Link>
+          <Link to="/tasks" className="text-sm opacity-80">Tasks</Link>
+          <Link to="/posts" className="text-sm opacity-80">Posts</Link>
+        </div>
+        <div className="flex items-center gap-2">
+          <Button variant="secondary" onClick={toggle}>
+            {theme === 'dark' ? 'Light' : 'Dark'}
+          </Button>
+        </div>
+      </div>
+    </nav>
+  )
+}
+
+diff --git a/src/components/Footer.jsx b/src/components/Footer.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/components/Footer.jsx
+@@ -0,0 +1,12 @@
+import React from 'react'
+
+export default function Footer(){
+  return (
+    <footer className="mt-8 py-6 border-t dark:border-gray-700">
+      <div className="max-w-6xl mx-auto text-center text-sm opacity-80">
+        © {new Date().getFullYear()} Your Name · Built with React + Tailwind
+      </div>
+    </footer>
+  )
+}
+
+diff --git a/src/components/Layout.jsx b/src/components/Layout.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/components/Layout.jsx
+@@ -0,0 +1,14 @@
+import React from 'react'
+import Navbar from './Navbar'
+import Footer from './Footer'
+
+export default function Layout({ children }){
+  return (
+    <div className="min-h-screen bg-gray-50 dark:bg-gray-900 text-gray-900 dark:text-gray-100 transition-colors">
+      <Navbar />
+      <main className="max-w-6xl mx-auto p-4">{children}</main>
+      <Footer />
+    </div>
+  )
+}
+
+diff --git a/src/hooks/useLocalStorage.js b/src/hooks/useLocalStorage.js
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/hooks/useLocalStorage.js
+@@ -0,0 +1,22 @@
+import { useEffect, useState } from 'react'
+
+export default function useLocalStorage(key, initial){
+  const [state, setState] = useState(() => {
+    try {
+      const raw = localStorage.getItem(key)
+      return raw ? JSON.parse(raw) : initial
+    } catch { return initial }
+  })
+
+  useEffect(() => {
+    try { localStorage.setItem(key, JSON.stringify(state)) } catch {}
+  }, [key, state])
+
+  return [state, setState]
+}
+
+diff --git a/src/components/TaskManager.jsx b/src/components/TaskManager.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/components/TaskManager.jsx
+@@ -0,0 +1,60 @@
+import React, { useMemo, useState } from 'react'
+import useLocalStorage from '../hooks/useLocalStorage'
+import Button from './Button'
+import Card from './Card'
+
+export default function TaskManager(){
+  const [tasks, setTasks] = useLocalStorage('tasks_v1', [])
+  const [input, setInput] = useState('')
+  const [filter, setFilter] = useState('all')
+
+  const addTask = () => {
+    if (!input.trim()) return
+    setTasks(prev => [{ id: Date.now(), text: input.trim(), done: false }, ...prev])
+    setInput('')
+  }
+
+  const toggle = id => setTasks(prev => prev.map(t => t.id === id ? { ...t, done: !t.done } : t))
+  const remove = id => setTasks(prev => prev.filter(t => t.id !== id))
+
+  const filtered = useMemo(() => {
+    if (filter === 'active') return tasks.filter(t => !t.done)
+    if (filter === 'completed') return tasks.filter(t => t.done)
+    return tasks
+  }, [tasks, filter])
+
+  return (
+    <div>
+      <Card className="mb-4">
+        <div className="flex gap-2">
+          <input
+            value={input}
+            onChange={e => setInput(e.target.value)}
+            onKeyDown={e => e.key === 'Enter' && addTask()}
+            placeholder="Add task and press Enter"
+            className="flex-1 px-3 py-2 rounded border dark:border-gray-700 bg-gray-50 dark:bg-gray-800"
+          />
+          <Button onClick={addTask}>Add</Button>
+        </div>
+        <div className="mt-3 flex gap-2">
+          <Button variant={filter === 'all' ? 'primary' : 'secondary'} onClick={() => setFilter('all')}>All</Button>
+          <Button variant={filter === 'active' ? 'primary' : 'secondary'} onClick={() => setFilter('active')}>Active</Button>
+          <Button variant={filter === 'completed' ? 'primary' : 'secondary'} onClick={() => setFilter('completed')}>Completed</Button>
+        </div>
+      </Card>
+
+      <div className="space-y-2">
+        {filtered.length === 0 && <Card>No tasks yet.</Card>}
+        {filtered.map(task => (
+          <Card key={task.id}>
+            <div className="flex items-center justify-between">
+              <div className="flex items-center gap-3">
+                <input type="checkbox" checked={task.done} onChange={() => toggle(task.id)} />
+                <span className={`truncate ${task.done ? 'line-through opacity-60' : ''}`}>{task.text}</span>
+              </div>
+              <div className="flex gap-2">
+                <Button variant="danger" onClick={() => remove(task.id)}>Delete</Button>
+              </div>
+            </div>
+          </Card>
+        ))}
+      </div>
+    </div>
+  )
+}
+
+diff --git a/src/api/posts.js b/src/api/posts.js
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/api/posts.js
+@@ -0,0 +1,9 @@
+export async function fetchPosts({ page = 1, limit = 10, signal } = {}) {
+  const res = await fetch(`https://jsonplaceholder.typicode.com/posts?_page=${page}&_limit=${limit}`, { signal })
+  if (!res.ok) throw new Error('Failed to load posts')
+  return res.json()
+}
+
+diff --git a/src/components/PostsList.jsx b/src/components/PostsList.jsx
+new file mode 100644
+index 0000000..1111111
+--- /dev/null
++++ b/src/components/Post
