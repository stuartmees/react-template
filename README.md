# react-template

## Basic Javascript Set Up

initialize the npm project on the command line which will create a package.json file. Libraries (node modules) you install will appear here:

```
npm init -y
```

By giving it the `-y` shorthand flag, you are telling npm that it should take all the defaults.

Now create a directory for projects source code:

>  /src/src/index.js

Into the scripts attribute of the package.json add the the following key value pair:

```
"start": "node src/index.js"
```

Now running `npm start` form the command line will run `node src/index.js` which runs the code in the source file.

[Wieruch Guide](https://www.robinwieruch.de/javascript-project-setup-tutorial/)








