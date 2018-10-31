---

## Getting Started

Tools and Project Setup

+++

### React Developer Tools

Browser extension for Chrome, Firefox, etc.

![React Toolbar Prod](img/react-toolbar-prod.png)

![React Toolbar Dev](img/react-toolbar-dev.png)

+++?image=img/react-devtools-box.png&size=contain

@title[RDT on Production]

Note:

- React Dev Tools in Firefox viewing a site using production React
- Since it's using production React, component names are minified (hence 't', 'd', etc)
- Provides props, state, and context information about the selected Component
- Allows realtime editing of state entries for a Component

+++?image=img/react-devtools-irb.png&size=contain

@title[RDT on Development]

Note:

- React Dev Tools in Chrome viewing a site running development React
- Shows non-minified component names, making it easier to trace your DOM
- Similar to the default dev tools, you can select an element on the page to see the associated React Component
- "Real" DOM elements are in grey to indicate what was actually rendered by the virtual DOM element

+++

### Two Ways to Build a React App

- Create React App
- Our Own Gulpfile

+++

### Create React App

As simple as:

```
npx create-react-app my-app
cd my-app
npm start
```

+++

@title[CRA Structure]

```text
my-app/
├── README.md
├── node_modules/
├── package.json
├── public/
│   ├── index.html
│   └── favicon.ico
├── static/
│   ├── index.html
│   ├── main.<hash>.js
│   ├── main.<hash>.css
│   └── favicon.ico
└── src/
    ├── index.js
    ├── App.js
    ├── App.test.js
    ├── App.scss
    ├── Textarea.js
    ├── Textarea.test.js
    ├── Textarea.scss
    ├── SubmissionForm.js
    ├── SubmissionForm.test.js
    └── SubmissionForm.scss
```

@[5-7](Your public files that should be accessible by an end user)
@[8-12](`npm build` copies everything from public into static. Most CD workflows only deploy the contents of static)
@[10-11](Created on `npm build`, ES5 and CSS code that can be deployed for the browser)
@[13-23](Your application source code)
@[14](The entry point into your React bundle)
@[15,18,21](JSX source for components)
@[16,19,22](Jest unit tests)
@[17,20,23](SASS styles for each component)

+++

@title[Pros and Cons]

Pros

- Live Reload offers faster iteration time
- Automates package installation and upgrades

Cons

- Run two web servers (port 3000 and 8000) in tandem
- Run `gulp watch` to lint/unit test PHP code
- Run `npm build` before every deployment (even to dev)

+++

### Our Own Gulpfile

- Minor changes made to the build process to fully support React code
- Add a script tag to point to a React build bundle

+++

@title[Current App Structure]

```text
my-app/
├── README.md
├── gulpfile.js
├── composer.json
├── package.json
├── index.php
├── services.php
├── template.php
├── node_modules/
├── vendor/
├── config/
├── models/
├── routes/
├── public/
│   ├── bundle.js
│   └── bundle.css
├── js/
│   ├── index.js
│   ├── App.js
│   ├── App.test.js
│   ├── Textarea.js
│   ├── Textarea.test.js
│   ├── SubmissionForm.js
│   └── SubmissionForm.test.js
└── sass/
    ├── index.scss
    ├── App.scss
    ├── Textarea.scss
    └── SubmissionForm.scss
```

@[6,7,10-13](Standard backend code)
@[8](The only HTML view template that PHP renders)
@[13](JSON API endpoints that are consumed by React components)
@[14-16](Auto-generated ES5 and CSS code)
@[17-24](React components and Jest tests)
@[25-29](SASS file per component - no more "layout" files)

+++

@title[Pros and Cons]

Pros

- Familiar, only slight changes from existing application structures

Cons

- Not very "React-suggested" way of doing things
- Chase can't figure out how to get sourcemaps to work right @fa[frown-o]

+++

### Hybrid Solution?

- Still use Create React App to build frontend code
- Extend it for handling backend linting/testing during
- Still would require 2 ports to run locally

+++

@title[Hybrid App Structure]

```text
my-app/
├── package.json
├── composer.json
├── vendor/
├── node_modules/
├── static/
│   ├── index.html
│   ├── main.<hash>.js
│   └── main.<hash>.css
├── api/
│   ├── index.php
│   ├── config/
│   ├── models/
│   │   └── *.php
│   ├── routes/
│   │   └── *.php
│   └── tests/
│       └── *.php
└── src/
    ├── *.js
    ├── *.test.js
    └── *.scss
```

@[2-5](Keep dependency managers separate from the codebase)
@[6-9](Serve up a static index and React bundle to end users)
@[10-18](Bundle all PHP source and tests into a single "API" codebase)
@[19-22](Keep all frontend code together the CRA-way)

+++

### Other Ideas Welcome
