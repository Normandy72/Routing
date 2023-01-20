# Routing
### For routing we can use:
#### ngRoute
* Separate JS file.
* Developed by Google & community.
* No concept of UI state.
* Every route must be represented by a URL.
* No concept of nested views.
* OK for prototype projects.
#### ui-router
* Separate JS file.
* Developed by community.
* UI state in center. Can have a route with no unique URL for that route.
* URL routing is also supported. UI state is updated based on the URL.
* Neated views suppurted.
* Better choice for more serious projects.

### Steps to using routing
#### Step 1: Reference in HTML
```
<script src="lib/angular.min.js"></script>
<script src="lib/angular-ui-router.min.js"></script>
```
`<script src="lib/angular-ui-router.min.js"></script>` - reference _after_ angular
#### Step 2: Place ui-view Initial View Placeholder
```
<body>
    ...
    <ui-view>
        // content of a view will be loaded here
    </ui-view>
    ...
</body>
```
#### Step 3: Declare ui-router As a Dependency
`angular.module('App', ['ui.router']);`

`'ui.router'` - module name uses '.', not '-'
#### Step 4: Configure Routes in .config Method
```
angular.module('App')
.config(RoutesConfig);

RoutesConfig.$inject = ['$stateProvider', '$urlRouterProvider'];
function RoutesConfig($stateProvider, $urlRouterProvider){
    ...
};

...
$stateProvider
    .state('view1', {
        url: '/view1',
        template: '<div> ... </div>'
        // or
        // templateURL: 'view1.html'
    })

    .state('view2', {...});
```
`'view1'` - unique state name

` url: '/view1'` - _optional_ URL associated with the state

`template: '<div> ... </div>'` - contents of template will be inserted into `<ui-view>...</ui-view>`

`.state('view2', {...});` - state method is chainable

```
$urlRouterProvider
    .otherwise(''/view1');

...
$stateProvider
    .state('view1', {
        url: '/view1',
        ...
    });
```
***
#### _Summary_
* `ui-router` uses independent concepts for URL mapping and UI state representation.
* Configure ui-router in angular.config:
    * provide alternate URL mapping with `$urlRouterProvider.otherwise('alternateURL');`;
    * configure states with optional URLs using `$stateProvider.state('name', {url: '...', templateUrl: '...'})`.
* Use `<ui-view>` tag as placeholder for state-based UI.
* Use `ui-sref` attribute for constructing links and actions to configured states.
***