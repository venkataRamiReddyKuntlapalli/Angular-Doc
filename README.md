Updates from version to version in angular ??
stanalone component ??
signals ??
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

	In Angular, directives are used to extend the functionality of HTML elements by adding behavior to them. There are three main types of directives:

	a. Component Directives – These are the most common directives, essentially a combination of HTML templates and logic. Every Angular component is technically a directive.

	B. Attribute Directives – These modify the appearance or behavior of an element, component, or another directive. Examples include:

		NgClass (adds/removes CSS classes)

		NgStyle (applies inline styles)

		NgModel (enables two-way data binding)

	c. Structural Directives – These change the DOM layout by adding or removing elements. Examples include:

		NgIf (conditionally adds/removes elements)

		NgFor (loops through an array to generate elements)

		NgSwitch (conditionally renders elements based on a value)

5. Interceptors

	In Angular, an Interceptor is a powerful feature that allows you to modify HTTP requests and responses globally before they reach the server or the application. It is commonly used for:

		Authentication: Adding authorization headers to outgoing requests.

		Logging: Tracking API calls for debugging.

		Error Handling: Catching and processing errors before they reach the application.

		Caching: Storing responses to optimize performance
		
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

	In Angular, pure and impure pipes determine how frequently a pipe executes during change detection.

a. Pure Pipes (pure: true)
	Default behavior in Angular.

	Executes only when the input value changes.

	Efficient because it avoids unnecessary recalculations.

Example:

typescript
@Pipe({ name: 'uppercasePipe', pure: true })
export class UppercasePipe implements PipeTransform {
  transform(value: string): string {
    return value.toUpperCase();
  }
}
	This pipe runs only when the input string changes.

b. Impure Pipes (pure: false)
	Executes on every change detection cycle, even if the input remains the same.

	seful when dealing with mutable objects like arrays or objects.

	Can impact performance if overused.

Example:

typescript
@Pipe({ name: 'filterPipe', pure: false })
export class FilterPipe implements PipeTransform {
  transform(items: any[], searchText: string): any[] {
    return items.filter(item => item.includes(searchText));
  }
}
	This pipe runs every time change detection occurs, even if items hasn't changed.

# Key Differences
Feature		Pure Pipe				Impure Pipe
Execution	Only when input changes	Every change detection cycle
Performance	Optimized				Can be inefficient
Use Case	Immutable data			Mutable data (arrays, objects)


14. Change Detection

	In Angular, the change detection cycle is the process that updates the DOM when the application state changes. Angular runs change detection automatically, but understanding how it works can help optimize performance.

	# How Change Detection Works
		Angular uses Zone.js to track asynchronous operations (like user interactions, HTTP requests, and timers). When an event occurs, Angular checks for changes in component properties and updates the view accordingly.

		Change Detection Strategies
		Angular provides two strategies:

		Default (ChangeDetectionStrategy.Default) – 
			
			Runs change detection on all components whenever an event occurs.

		OnPush (ChangeDetectionStrategy.OnPush) – 
			Runs change detection only when input properties change, improving performance.

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

In Angular, route guards like CanActivate and CanLoad help secure routes by controlling access based on authentication, user roles, or permissions.

1. Implementing CanActivate (Restricting Route Access)
CanActivate prevents unauthorized users from navigating to a route.

Example: Authentication Guard

import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';
import { AuthService } from './auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}

  canActivate(): boolean {
    if (this.authService.isLoggedIn()) {
      return true;
    }
    this.router.navigate(['/login']);
    return false;
  }
}
Usage in Routing Module:

const routes: Routes = [
  { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }
];
2. Implementing CanLoad (Restricting Lazy-Loaded Modules)
CanLoad prevents unauthorized users from loading an entire module.

Example: Lazy Loading Guard

import { Injectable } from '@angular/core';
import { CanLoad, Route, Router } from '@angular/router';
import { AuthService } from './auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthLoadGuard implements CanLoad {
  constructor(private authService: AuthService, private router: Router) {}

  canLoad(route: Route): boolean {
    if (this.authService.isLoggedIn()) {
      return true;
    }
    this.router.navigate(['/login']);
    return false;
  }
}
Usage in Routing Module:

typescript
const routes: Routes = [
  { path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule), canLoad: [AuthLoadGuard] }
];
Key Differences:

Feature		CanActivate							CanLoad
Purpose		Prevents unauthorized navigation	Prevents unauthorized module loading
Use Case	Protects individual routes			Protects lazy-loaded modules
Execution	Runs before navigation				Runs before module loading
Performance Impact								Minimal	Prevents unnecessary module loading


Guard				Purpose								Use Case
CanActivate			Restricts route access				Authentication
CanActivateChild	Restricts child routes				Admin panel
CanLoad	Prevents 	lazy-loaded module access			Secure module loading
CanDeactivate		Prevents navigation away			Unsaved form warning

   this.settingsForm = this.fb.group({
      username: [''],
      email: ['']
    });

    this.settingsForm.valueChanges.subscribe(() => {
      this.unsavedChanges = true;
    });
  }

  hasUnsavedChanges(): boolean {
    return this.unsavedChanges;
  }
  
Resolve				Pre-fetches data before navigation	Load user data before profile page
CanMatch			Dynamically matches routes			Role-based routing

Which Guard Should You Use?
For authentication → Use CanActivate

For admin sections → Use CanActivateChild

For lazy-loaded modules → Use CanLoad

For unsaved changes → Use CanDeactivate

For pre-fetching data → Use Resolve

For dynamic route matching → Use CanMatch

19. diff b/w observables & subjects:
20. new ES6 features in JS
	1. let and const for Variable Declaration
		let allows block-scoped variables.

		const defines constants that cannot be reassigned.
			let name = "John";
			const age = 30;

21. Dependency injection:
22. NGRXJS

