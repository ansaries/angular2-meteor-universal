# Angular2-Universal-Meteor

Porting of Angular2-Universal for Angular2-Meteor based on FlowRouter.

## Usage

There are several points to consider before using this library:

- These two Atmosphere packages are a prerequisite:
  `angular2-runtime` and `kadira:flow-router-ssr`.

- Angular 2 components that you want to render both on the client and server parts should be placed
  in the 'imports' folder and imported from there;

- Routing is based on the FlowRouter package. In order to add routers, 
  create a `route.ts` file at the root level of your app and
  start adding URLs of the main Angular2 components you want to be pre-rendered on the server side.
  Use `Router.route` and `Router.group` to add routers and groups of the routes
  as you can see here [route.ts](./examples/app/route.ts);

- If your main app component has own Angular 2 routing (i.e., based on `RouteConfig`),
  you'll need to create a FlowRouter's routing group, like [here](./examples/app/route.ts#L21),
  and add paths that you want to pre-render on the server side.
  Please note that you'll need to set `target` attribute of the `a` links to either `_blank` or `_top`
  in order to reload current page with a new component on it which has been pre-rendered on the server.
  Otherwise, Angular 2 will load components dynamically w/o reloading the page, thus,
  bypassing the server;

- If you want to render some component on the client side only, then you
  need to work with the `client` folder as most of you do regularly by 
  putting there Angular 2 components, and also create `routes.ts` there with client side routes;

- `Router.route` and `Router.group` are only wrappers over analogous methods of  `FlowRouter`, 
  so they take same parameters as original methods. If want to use other methods of the `FlowRouter`'s API ,
  do it in the same way as described in the `FlowRouter` [docs](https://github.com/kadirahq/flow-router);

- Having ability to define different routes for different Angular 2 components and pre-render
  them on the server side, allows us to have multiple Angular 2 apps in one Meteor app structure.
  Please, check out a demo app in `example/app` folder that have two Angular 2, Socially and TODO, components
  that you can load separately at different `/parties` and `/todo` routes accordingly.
