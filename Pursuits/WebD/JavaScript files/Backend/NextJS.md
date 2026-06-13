# Next.js

- **File-Based Routing (No React Router Needed)**
    
    - Pages are automatically created based on the file structure inside `/pages`.
        
    - Example: `pages/about.js` → accessible at `/about`.
        
- **Server-Side Rendering (SSR)**
    
    - React by default is **client-side rendered** (CSR).
        
    - Next.js can render pages on the **server first**, which makes apps faster and SEO-friendly.
        
- **Static Site Generation (SSG)**
    
    - Pre-generates HTML at build time for performance.
        
    - Example: Blogs, docs, landing pages.
        
- **Incremental Static Regeneration (ISR)**
    
    - Regenerates static pages in the background after a given time.
        
    - Combines benefits of **static + dynamic** content.
        
- **SEO Friendly by Default**
    
    - Because of SSR & SSG, search engines see fully rendered pages (not just empty `<div>` with JavaScript).
        
- **API Routes (Backend Built-In)**
    
    - You can create backend endpoints inside `/pages/api/*`.
        
    - Example: `pages/api/users.js` → `/api/users`.
        
    - Removes the need for a separate backend in many cases.
        
- **Image Optimization**
    
    - Built-in `<Image />` component optimizes images (resizing, lazy loading, compression).
        
- **Code Splitting & Automatic Optimization**
    
    - Only loads the JavaScript needed for the current page.
        
    - Improves page load speed.
        
- **Built-in CSS & Styling Options**
    
    - Supports CSS Modules, Sass, Tailwind, Styled Components, etc.
        
    - Scoped styles are super easy.
        
- **TypeScript Support Out of the Box**
    
    - Just add `tsconfig.json` and Next.js configures everything.
        
- **Middleware**
    
    - Lets you run code **before a request is completed** (auth, redirects, logging).
        
- **Edge & Serverless Functions**
    
    - Deployable to serverless platforms (like Vercel, AWS Lambda).
        
    - Reduces backend complexity.
        
- **Performance Optimizations by Default**
    
    - Prefetching of linked pages.
        
    - Compression & caching.
        
    - Automatic static optimization.
        
- **Hybrid Rendering**
    
    - You can mix SSR, SSG, and CSR in the same app depending on the page’s need.
        
- **Easy Deployment (especially with Vercel)**
    
    - Next.js is made by Vercel, so deployment is one-click.
        
    - Serverless functions + edge caching are integrated.


# How to setup Next.js

- Use `npx (node package executable)`.
- We can do it  with npm as well but that installs all dependencies in our drives but if we use npx then it downloads and executes the dependencies on runtime and then remove it from the system. We only require 3 dependencies (react , react-dom, next).
- Write command `npx create-next-app@latest`.
	- It creates it
- It will ask you what dependencies you would like to use
	- TypeScript
	- Tailwind CSS
- Next.js is a framework which supports frontend of website for server side handling.
- Application runs on browser but node.js run on your OS and interacts with it and Next.js runs on top of node server.
- Next.js is  a frontend framework that do a lot of things on server side also.
- Next.js is a framework but it also has next.js library
- Next.js compile the code and runs the code on node.js of server before serving to frontend of client and hence client's browser did not require to render the code.
- Earlier when using react browser has to handle everything from using babble to convert jsx to js and then render it on client side.

- Scripts have shortcuts to run on terminal.
	![[Pasted image 20251011101542.png|200]]
	- One of such script to run the project is `npm run dev` which build the application and host on node.js and runs it on 3000 port.
	- After executing the command you will find compiles the code before rendering.
- Initially the content inside page.js is rendering.
- Next.js renders each and every component on server side but  in case we don't want that we have to specify if that component should be rendered on client side.
- So by default server side rendering is in action
![[Pasted image 20251009203858.png]]
![[Pasted image 20251009204032.png]]

- We can't use `useEffect()` hook as it is used to make changes at client side but next.js try to do this at the server side which gives this error.
- 
![[Pasted image 20251009204830.png]]


---

- Entry point of a Next.js file is `layout.js`.
- It is mandatory the name of file is `layout.js` and similarly for `page.js`.

![[Pasted image 20251011100109.png|200]]
- Why segregation between dependencies and devDependencies. How they are different?
	- They **both define packages** your project uses but they differ in **when and why** they are needed.
	- [[Differences between dependencies and devDependencies]]
- `npm run dev` runs the `next dev` script which basically builds the html out of the files and run next inside node

![[Pasted image 20251011100153.png|200]]
- `postcss` is used to compile the tailwind


![[Pasted image 20251011100239.png|250]]


- Now it has become global convention to use `favicon.ico` which can be used to put an image at tab except from icons.


![[Pasted image 20251011102344.png|300]]


- Running the dev command build html inside of server in .next folder.


![[Pasted image 20251011104004.png]]



To deploy use `npm run build`
To develop use `npm run dev`

webpack - bundler tool that is installed by next.js internally and used to compile the code.


# Routing
- Next.js uses file based routing.
- It is mandatory to use page.js for routing as it provides export default functionality.

- Default Keyword
	![[Pasted image 20251011104355.png|300]]
	- There could be multiple exports but only one default export.
	- It exports the component at runtime.
	- Without default export layout.js cannot find the Component and throws error.
	- It allows that while importing the Component you can give any name to that component.



Now we know how to create route , now lets see how to move to routes

![[Pasted image 20251011112922.png|300]]
![[Pasted image 20251011112943.png|200]]
- Whenever i click the link it takes to that path like we have visited for first time and hence the page was reloading when we visit.



- Now in react we divide the page in three parts.
	- header
	- main (it's dynamic in nature)
	- footer
- So the problem is when we move to different page it refresh which hinders the user experience although next.js is theoretically single page application.
- Next.js is always a single page application but how we achieve it can vary.
- Hence we cannot use anchor tag as it always refreshes the application.
- Therefore we use `Link` which is a Next.js component.
	![[Pasted image 20251011113707.png|300]]
	![[Pasted image 20251011113859.png]]

- What Link component does it when we first visit a new page it reloads it after making request to server. But then `webpack-hmr` stores some data about that page so in case the same page is visited again then it will use the concept of `prefetching` and just renders the page without reloading. Prefetching works only at production not in developer mode.
- First time component is rendered at server side then that rendered component is sent as RSE-Payload (in format of json file) or SSR HTML.


- Which URL's are not prefetched in Next.js?
	- External URL's which are of some external website are not prefetched and their is no benefit of prefetching those page as well.

- Hydration (happens while rendering)
	- It happens in browser after server side rendering, some chunks in that SSR HTML page is rendered from client side which is called hydration and in a way both are combined to  provide a consistent UI as expected by the user.

- Using Link component it executes the 90% of server side rendering in background when Link is rendered in the frontend. So it optimizes the re-rendering of visited component. Although it makes the frontend page rendering a little slow. So prefetching is preponing the rendering part of server side to the Link component.



# Production side build

- Run `npm run build`

![[Pasted image 20251018201640.png|300]]
![[Pasted image 20251018201642.png|300]]

- Then run` npm run start` to send build to run in node.js
- Pre-rendering words only in production mode and not developer mode.


# Client Side Component
- Component rendered and running on browser.

# Server Side Component
- Component rendered and running on Server

![[Pasted image 20251113210931.png]]
# Directive
- Here  client directive is used to tell NodeJS to keep the component as client side component although it is still being rendered on server by NodeJS but it skips the part which is to be rendered at client side. Later NodeJS will know that it needs to combine the hydration part from client side to rendered component from server side.
![[Pasted image 20251018203000.png|300]]

- Event Handlers cannot run in NodeJS as it's a browser thing hence we need to use directive.
![[Pasted image 20251018203433.png]]
- Similarly `localStorage`, web api's like `setTimeOut` runs on browser , hence they don't work on Server Side.
- After adding directive if client side code is inside jsx code then that will run fine but if something like `localStorage` is used outside of jsx then it will still throw error
	![[Pasted image 20251018203947.png|300]]
	- Now  we have to use `useEffect` to prevent the rendering of `localStorage` in this case on server.
	![[Pasted image 20251018203957.png|300]]
- If one want's specific component to be rendered then position the `use client;` just before that component.
# Image tag
- React gives its own Image tag



# Industry Practices
- Use `/p` before products to signify product listing
![[Pasted image 20251018211635.png]]
- Similarly use `/c` to signify categories.
- Create p folder and inside it in react if we create dynamic routes then to signify that we use `[]` square brackets, inside which you can write anything but industry convention many times one uses `slug`. Inside this now you can create pages.
	![[Pasted image 20251018211956.png|100]]
	![[Pasted image 20251018211933.png|100]]

- Due to server side rendering if you do console.log it will be visible on server side not browser side.
- Since there are lot of things logged in server side hence often we use dashes to find the log.
	![[Pasted image 20251018212353.png|300]]

- In case you want dynamic nested routes then we use spread operator before the name.
	![[Pasted image 20251018213219.png|300]]


# How to add meta data to show description over the document

![[Pasted image 20251018213736.png]]
Read about RSC Payload
Bundler

outer parenthesis show it's an expression and inner parenthesis denotes the style object.
- Conventionally `global.css` file is used for global css and they are put inside the layout (layout.js) file in root (app).
- In public folder we usually puts assets like images, video, audio, fonts etc.
- 


# Default exports vs named Export
- If we use default to export the file then you can import that file with any name.
- In case of named Export we don't use default keyword (like export function ()), now to import this you need to specify the same name of function you are tying to import inside the curly braces.


> NextJS uses `file based` routing.

- To use browser 

# Simulating sleep behavior
![[Pasted image 20251101110521.png]]
Component should be Async in case some method in it using asynchronous operation.



# Conditional Rendering


Example of Conditional based Rendering
![[Pasted image 20251106212307.png]]
- Here After && code is rendered in case variant matches to primary in this case.
- To show a loading screen before all products are fetched. Use `Suspense` component.
	![[Pasted image 20251101115532.png|400]]
- To fetch path at server side
	- `use` hooks work at client side so it can not be used at server side.



>[Resource](https://styled-components.com/)

> By default react builds a not-found page but we have to do handling so that in case of wrong link it leads to not found page.
> 
# Server Side Rendering
- On demand Server side rendering
	- Here we are saving the time which is taken by client side to render.
	- After server renders then push the page on client side.
	![[Pasted image 20251106203433.png]]
	- Now it's a dynamic page and will take 10 seconds to render each time
	- The problem with this it always will be rendered again.
- Pre rendering on server side.
	- After a dynamic page is rendered/build and then saved , if again someone calls the page then it will be served as static page.
	![[Pasted image 20251106203204.png]]
	- It takes 10 second for the first time only
	- Problem with this is in case backend data changes then it is not reflected in static page.

Checked using `npm run build`
![[Pasted image 20251106202532.png|300]]

- Now how to get the best of both world
	- Set time after which cache will update it's content to account for updated data, so like refreshing the page like 10 times will lead to loading the updated data.
![[Pasted image 20251106204512.png|400]]
![[Pasted image 20251106204449.png]]
- Never used in PDP (Product details page) - product information + product price + product stock level.
	- This is bcz prices can change very often, no. of products is very high therefore they are rendered by server on demand.
- But best examples are:
	- Home page - This can be prerendered (most accessible + no transactions) revalidate in 15 minutes
	- Block page - This can be prerendered (most accessible + no transactions) Revalidate in 15 minutes  
- Page level loaders are used in very niche use cases.


> [Resource](https://flowbite.com/docs/components/buttons/)
> components, forms


- Login page is a good candidate for static page so no need to revalidate.pre