# NPM Interview Questions

> **Level:** Fresher / Junior Developer
> **Focus:** NPM fundamentals required for JavaScript, React, and Node.js projects
> **Goal:** Understand how dependencies and project packages are managed.

---

# 1. What is NPM?

NPM stands for **Node Package Manager**.

It is the standard package manager commonly used with Node.js projects.

NPM helps developers:

* Install packages
* Remove packages
* Update packages
* Manage dependencies
* Run project scripts
* Share packages

Example:

```bash
npm install express
```

---

# 2. What is `package.json`?

`package.json` is the main configuration file for an NPM project.

It contains information such as:

```text
Project name
Version
Scripts
Dependencies
Dev dependencies
```

Example:

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "scripts": {
    "dev": "nodemon server.js",
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^5.0.0"
  }
}
```

---

# 3. What is `package-lock.json`?

`package-lock.json` records the exact dependency versions resolved for the project.

It helps ensure that installations are more reproducible across different environments.

Simple difference:

```text
package.json
→ What packages the project needs

package-lock.json
→ Exact dependency tree that was resolved
```

---

# 4. What is `node_modules`?

`node_modules` is the directory where installed packages are stored.

Example:

```text
project/
├── node_modules/
├── package.json
└── package-lock.json
```

Normally, `node_modules` should not be committed to Git.

Add it to:

```gitignore
node_modules/
```

---

# 5. How do you create a new NPM project?

Run:

```bash
npm init
```

Or:

```bash
npm init -y
```

`-y` accepts the default values and creates `package.json`.

---

# 6. How do you install a package?

```bash
npm install express
```

Short form:

```bash
npm i express
```

The package is added to `dependencies`.

---

# 7. How do you install a development dependency?

```bash
npm install nodemon --save-dev
```

Short form:

```bash
npm i nodemon -D
```

Development dependencies are generally tools needed during development rather than runtime.

Examples:

```text
nodemon
eslint
prettier
testing tools
```

---

# 8. Dependencies vs devDependencies

### dependencies

Required by the application at runtime.

Example:

```json
"dependencies": {
  "express": "^5.0.0",
  "mongoose": "^8.0.0"
}
```

### devDependencies

Primarily required during development.

Example:

```json
"devDependencies": {
  "nodemon": "^3.0.0"
}
```

---

# 9. What is `npm install`?

Running:

```bash
npm install
```

installs the dependencies described by the project configuration and lockfile.

This is commonly the first command after cloning a Node.js project.

Typical flow:

```text
git clone
    ↓
npm install
    ↓
npm run dev
```

---

# 10. How do you uninstall a package?

```bash
npm uninstall express
```

Short form:

```bash
npm remove express
```

---

# 11. How do you update a package?

You can use:

```bash
npm update
```

For a specific package:

```bash
npm update express
```

For major version upgrades, check the package's release notes and compatibility requirements before upgrading.

---

# 12. What are NPM scripts?

Scripts are commands defined inside `package.json`.

Example:

```json
{
  "scripts": {
    "dev": "nodemon server.js",
    "start": "node server.js",
    "test": "jest"
  }
}
```

Run them using:

```bash
npm run dev
```

For some standard scripts such as `start`:

```bash
npm start
```

---

# 13. What is `npm start` vs `npm run dev`?

This depends on the scripts defined by the project.

Example:

```json
{
  "scripts": {
    "dev": "nodemon server.js",
    "start": "node server.js"
  }
}
```

Then:

```bash
npm run dev
```

starts the development server with Nodemon.

```bash
npm start
```

starts the application using Node.js.

---

# 14. What is semantic versioning?

Packages commonly use:

```text
MAJOR.MINOR.PATCH
```

Example:

```text
2.4.1
```

Means:

```text
2 → Major
4 → Minor
1 → Patch
```

Generally:

```text
Major
→ Potentially breaking changes

Minor
→ New backward-compatible features

Patch
→ Bug fixes
```

---

# 15. What does `^` mean in package versions?

Example:

```json
"express": "^5.0.0"
```

The version range allows compatible updates according to semantic-versioning rules, generally allowing minor and patch updates within the same major version.

The exact resolved version is recorded in the lockfile.

---

# 16. What is `npx`?

`npx` is used to execute packages, commonly without requiring a global installation.

Example:

```bash
npx create-vite@latest
```

Another example:

```bash
npx eslint .
```

Simple difference:

```text
npm
→ Manage/install packages

npx
→ Execute a package
```

---

# 17. Global vs local package installation

Local:

```bash
npm install nodemon
```

The package belongs to the project.

Global:

```bash
npm install -g nodemon
```

The package is installed globally for the environment.

For project dependencies and reproducible development, local installation is generally preferred.

---

# 18. How do you check installed packages?

```bash
npm list
```

For a specific package:

```bash
npm list express
```

You can also inspect:

```text
package.json
package-lock.json
```

---

# 19. What is `npm audit`?

`npm audit` checks the project's dependency tree for known security vulnerabilities reported by NPM's advisory data.

Run:

```bash
npm audit
```

Possible automatic fixes:

```bash
npm audit fix
```

Always review changes after automatic dependency updates.

---

# 20. What happens when you clone an NPM project?

Usually:

```text
Clone repository
      ↓
cd project
      ↓
npm install
      ↓
Dependencies installed
      ↓
npm run dev
```

You generally do not clone `node_modules` from Git.

---

# NPM Revision Checklist

* [ ] What is NPM?
* [ ] `package.json`
* [ ] `package-lock.json`
* [ ] `node_modules`
* [ ] `npm init`
* [ ] `npm install`
* [ ] `npm uninstall`
* [ ] dependencies
* [ ] devDependencies
* [ ] NPM scripts
* [ ] `npm start`
* [ ] `npm run dev`
* [ ] Semantic versioning
* [ ] `npx`
* [ ] Local vs global packages
* [ ] `npm audit`

---

# NPM Project Flow

```text
Create Project
     ↓
npm init
     ↓
package.json
     ↓
npm install
     ↓
node_modules
     ↓
package-lock.json
     ↓
npm run dev
```

### One-Line Interview Answer

> **NPM is the package manager used to install, manage, execute, and maintain dependencies and scripts in Node.js projects.**
