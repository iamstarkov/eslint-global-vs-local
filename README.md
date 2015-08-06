# eslint-global-vs-local

global eslint cannot see local packages. And it kinda wrong: other tools like mocha, karma, grunt and gulp, user local versions of itself if it exists.

You can see the problem. You can run `eslint index.js` and `npm run eslint` in this repo. Obviously, run `npm install` at the start.

_index.js:_

    var some = '';

which violate airbnb codestyle. _.eslintrc:_

    { "extends": "eslint-config-airbnb" }

_package.json scripts field:_

      "scripts": {
        "eslint": "eslint index.js"
      },

## summary

local copy of eslint runned from npm-scripts works well. global one throw an error. from my perspective of other tools, its wrong.

```
➜  eslint-global-vs-local git:(master) ✗ eslint index.js
/usr/local/lib/node_modules/eslint/lib/config.js:141
                    throw e;
                          ^
Error: Cannot find module 'eslint-config-airbnb'
Referenced from: /Users/matmuchrapna/projects/eslint-global-vs-local/.eslintrc
    at Function.Module._resolveFilename (module.js:336:15)
    at Function.Module._load (module.js:286:25)
    at Module.require (module.js:365:17)
    at require (module.js:384:17)
    at loadConfig (/usr/local/lib/node_modules/eslint/lib/config.js:104:48)
    at /usr/local/lib/node_modules/eslint/lib/config.js:135:46
    at Array.reduceRight (native)
    at loadConfig (/usr/local/lib/node_modules/eslint/lib/config.js:119:36)
    at getLocalConfig (/usr/local/lib/node_modules/eslint/lib/config.js:243:23)
    at Config.getConfig (/usr/local/lib/node_modules/eslint/lib/config.js:371:22)
```
