# General best practices

## 1 - Using Husky (Git Hooks) to validate some things important to your project as:
* Run Lint before every commit.
* Run tests before every push.


This way can help your team to keep the codes with very best practices in JS.

### How to configure this:

Inside your project run the following.

```bash
  $ npm install --save-dev husky  
```
Then, in `package.json` scripts section, add the following scripts.

```json
   "scripts": {
    "precommit": "npm run lint",
    "prepush": "npm run tests",
    "tests": "ng test",
    "lint": "ng lint"
  },
```

This way, the lint task will be executed before every commit and the test task before every push.

Thanks to [Mateus Durães](https://github.com/mateusduraes), Pluriworker Developer Front by found out this great tool to improve our projects!

---

## 2 - Comming Soon:
