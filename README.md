* Create a new folder, open in VS code
* In terminal enter this cmd `# go mod init <module-name>`, it will create go.mod file
* go.mod file will tell us module name, go version, and any dependent module we will use
* Create cmd/web folder - If we want to have web pages served, we will typically keep them here. This is the norm in golang projects
* Inside that create a main.go file
* Now here we will create a simple webserver, that listens to requests
* **Extra Info** - Now in production you typically be listening on port 80 for a web server if it's insecure connections, and port 443 if it's using secure connections i.e. Https.
* So for our dummy projects we typically we listen on one of the unprivileged ports, anything that's not commonly used, above port 1024. Here lets take 4000. When initializing always use colon v.v.imp
* There are certain kinds of information that we want to share with other parts of the application. For example, connection to the database, any command line parameters that we want to specify at runtime that sort of thing. So how can we do that?  By creating our own type. `type app struct {}`
* **Note** - Inside of this struct is where we'll be specifying things like what's our database model, what's our pool of database connections, that sort of thing. Now when we go a little bit further in this course, we're going to move this type to its own package.
* Lets set up a web server, step by step and easely
* Lets create a handler, using inbuilt http.Handlefunc, and a listenandserve func and error handling
* Once done, run it using - `# go run ./cmd/web` 
* To exit - ctrl + C
* In this application we're using something called the default serve mux, built into the standard library, when we call the HTTP package and call handle func, we're registering a route called slash(/) that executes this inline function.
* Similarly we can put all of our routes in this way inline or individual functions. But there are some drawbacks to it. 
* For example, 404 page not found. That doesn't work by default without some some actual code written to handle that situation. For that we have to use a third party routing package, and there are many to choose from in the go world.
* We are using Chi router - `# go get -u github.com/go-chi/chi/v5`, check go.mod it will be added there as an indirect dependency.
* **Extra Info** When you have a major version change in go, it typically means that it's not backwards compatible.
* Next we will use another package from chi, middleware `# go get -u github.com/go-chi/chi/v5/middleware` It's something that sits between the the router and the handler. It allows us to manage the request in various ways.
* For example if something crashes, if there is a problem with one of the handlers that We'll be adding later on, we don't want the entire application to die. we don't want it to panic. we want it to recover.
