This is a starter template for [Learn Next.js](https://nextjs.org/learn).

# Nextjs tutorial by Vercel
## Basics
1. another tutorial wo magic [Nextjs intro | Auth0](https://auth0.com/blog/next-js-practical-introduction-for-react-developers-part-1/)
2. `"scripts": { "dev": "next", "build"...,"start"..."`
3. Add ./pages/index.js - 
4. `const Index = () => (<div> <p>Thank you, next</p> </div> ); export default Index;`
5. With Next.js, you can think of the `App.js` component as being implied thru `./pages` and hierarchy
6. create the uniform core interface w 3 components: `[layout, header, navbar]`
7. In Layout.js, ... render any content passed through **props.children** within a Content container -
8. `const Layout = props => ( <div className="Layout" style={layoutStyle}>`
    `<Header /> <div className="Content" style={contentStyle}> {props.children} </div> <NavBar /> </div> );`

### Code through API routes
#### ./components/date
1. Accepts data string param
2. returns formatted date

#### ./components/layout.js
1. `import ...next/head`
2. built-in **Nextjs** component for appending elements to head of the page
3. [Next-Head](https://nextjs.org/docs/api-reference/next/head)
4. to avoid duplicate tags in your head you can use the key property
5. `<meta property="og:title" content="My page title" key="title" />`
6. The contents of head get cleared upon unmounting the component, so make sure each page completely defines what it needs ...
7. **Note:** ...to link to an external page outside the Next.js app, use an `<a>` tag without Link

#### ./posts/file1 file2...
1. pages/posts/[id].js reads this directory to find files to "slurp in"


#### pages/posts/[id].js
1. Hold the blog posts
2. `export default function Post({ postData }) {`
3. Fed by props ... external data files
4. blog posts written in markdown are parsed
5. `getStaticProps` does some work
6. `lib/posts` takes part of the workload
7. Posts function then formats
- date
- title
- content
8. and styles it - `className={utilStyles.headingXl}`
9. filename is - postData.id
10.  in Next.js, when you export a page component, you can also export an async function called getStaticProps
11. Essentially, `getStaticProps` allows you to tell Next.js: “... this page has data dependencies, ... 
12. when you pre-render this page at build time, make sure to resolve them first!”

#### lib/posts
1. Get file names under /posts
2. `const fileNames = fs.readdirSync(postsDirectory)`
3. Remove ".md" from file name to get id
4. Read markdown file as string
5. Use gray-matter to parse the post metadata section

#### pages/_app.js
1. Nextjs custom `App` component
2. [Custom App](https://nextjs.org/docs/advanced-features/custom-app)
3. Next.js uses the App component to initialize pages. 
4. override it and control page init; Which allows you to do amazing things like:
- Persist layout btwn page changes
- Keep state when navigating pages
- Custom error handling w `componentDidCatch`
- Inject additional data into pages
- Add global CSS
5. To override the default App, create `./pages/_app.js`
6. **Component prop** is the active page,
7. `export default function App({ Component, pageProps })`
8. so whenever you navigate between routes, Component will change to the new page
9. any props you send to Component will be received by the page

##### Nextjs - Layout persistence
1. [Layout persistence in Nextjs](https://dev.to/ozanbolel/layout-persistence-in-next-js-107g)
2. using custom component "_app.js" w initializing process of the application, and 
3. can contain [inject?] the page component in the layout component
4. add layout components ... directly to the page components
5. `export default function MyLayout({ children }) {`
6. return statement for **MyLayout**
7. `<p> <button onClick={() => setCounter(counter + 1)}>
   Clicked {counter} Times
   </button> </p> {children}`
8. when you create sample pages under “./pages” - “/pages/profile.js”, add layout -
9. `Profile.Layout = MyLayout;`
10. ... The counter didn't reset during routing because these two pages share the same layout component. If I go to a different page, MyLayout will be unmounted and the counter will reset
11. this is **Option 3: Add a static `layout` property** to page components from Adam W; see #1 above



#### pages/index.js
1. The Page component receives PostsData prop at **build time**

## Thu, Mar 10
1. Changed text color to test git push
