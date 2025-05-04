Life cycle hooks: ??

1. Local storage & cookie storage
Ans: 
	Local Storage is straightforward and allows you to store larger amounts of data, making it suitable for application state and user preferences.

	localStorage.setItem(key, JSON.stringify(value));
	JSON.parse(localStorage.getItem(key) || '{}');
	localStorage.removeItem(key);
	locaStoraage.clear();

	Cookies are ideal for small amounts of data that need to be sent to the server, such as session identifiers. Using a library like ngx-cookie-service simplifies cookie management in Angular.

	npm install ngx-cookie-service
	
2. Decorators:

Ans:
In Angular, decorators are special functions that attach metadata to classes, methods, properties, or parameters. They are a feature of TypeScript and are prefixed with the @ symbol. Decorators play a crucial role in defining the structure and behavior of Angular applications.

Here are the main types of Angular decorators:

Class Decorators:

	@Component: Defines a component and its metadata, such as template and styles.

	@NgModule: Defines a module and its metadata, like declarations and imports.

Property Decorators:

	@Input: Marks a property as an input binding, allowing data to be passed into a component.

	@Output: Marks a property as an output binding, enabling event emission.

Method Decorators:

	@HostListener: Listens to events on the host element, such as clicks or mouse movements.

Parameter Decorators:

	@Inject: Specifies a dependency to be injected into a constructor.

Decorators are essential for Angular's dependency injection, component creation, and event handling.

3. Forms
4. Directives: https://v17.angular.io/guide/architecture-components#directives
5. Interceptors
6. How angular app runs in the DOM while loading in browser
7. Authentication & Authorization
8. Diff ng build & ng serve
9. How ng build works -> how it create dist.
10. CORS error why? how to resolve?

CORS (Cross-Origin Resource Sharing) errors occur when your Angular application tries to make a request to a different origin (domain, protocol, or port) than the one from which it was served. This is a security feature implemented by browsers to prevent unauthorized requests.

Server-Side Changes: The most reliable solution is to configure the server to allow cross-origin requests. The server needs to send specific CORS headers in its response. Common headers include:

Steps to Set Up a Proxy from Ui to access 3rd party api:
  origin: 'http://localhost:4200', // or '*' to allow all
  methods: 'GET,POST',
  allowedHeaders: 'Content-Type,Authorization'
Create a file named proxy.conf.json in your Angular project root:
{
  "/api": {
    "target": "http://api.example.com",
    "secure": false,
    "changeOrigin": true,
    "logLevel": "debug"
  }
}

Update your angular.json file to include the proxy configuration in the serve section:
"architect": {
  "serve": {
    "options": {
      "proxyConfig": "proxy.conf.json"
    }
  }
}

11. How to improve the performance of an application?

     a. Lazy loading.
     b. Tree shaking
Build with Production Flag: Use ng build --prod for tree shaking.
Use ES Modules: Stick to ES6 module syntax.
 Ensure that you are using ES6 module syntax (e.g., import and export). Tree shaking works by analyzing the import/export statements, so using CommonJS (require/export) will not allow for effective tree shaking.
Check angular.json: Ensure optimization settings are enabled.
Manage Side Effects: Use the sideEffects field in package.json wisely.
Implement Code Splitting: Use lazy loading for modules.

12. Smart component & Dumb component

Ans: 
In Angular, the concepts of Smart Components and Dumb Components are design patterns that help organize and structure applications effectively.

a. Smart Components
	Purpose: Handle application logic, manage state, and interact with services.

	Responsibilities:

		Fetch data from APIs or services.

		Process and manage application state.

		Pass data to dumb components via @Input bindings.

		Handle events emitted by dumb components via @Output.

	Example: A component that fetches a list of items from a server and passes it to a child component for display.

b. Dumb Components
	Purpose: Focus solely on presentation and rendering UI.

	Responsibilities:

		Receive data via @Input bindings.

		Emit events via @Output bindings.

		Avoid direct interaction with services or application logic.

	Example: A component that displays a list of items passed to it by a parent component.

13. Pure pipe & Impure pipe
14. Change Detection
15. sync / Async pipes
16. AOT & JIT compiler

Ahead-of-Time (AOT) Compilation:

AOT compiles the application during the build process, which results in faster rendering in the browser and smaller bundle sizes.
Just-in-Time (JIT) Compilation:

JIT compiles the application in the browser at runtime. It's mainly used during development for faster iterations.

17. Routing
18. Auth0:

Route guards in Angular are used to control access to routes based on specific conditions. They help in securing routes by allowing or preventing navigation to a particular route. Angular provides several types of guards:

CanActivate: Determines if a route can be activated.

CanActivateChild: Determines if a child route can be activated.

CanDeactivate: Determines if a route can be deactivated.

Resolve: Pre-fetches data before navigating to a route.

CanLoad: Determines if a module can be loaded lazily.

19. diff b/w observables & subjects:
20. new ES6 features in JS
21. Dependency injection:
22. NGRXJS

