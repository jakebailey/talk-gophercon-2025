---
theme: default
drawings:
  persist: false
  enabled: false
# transition: slide-left
transition: fade
# transition: fade-out
# transition: view-transition
canvasWidth: 980
mdc: true
download: true
exportFilename: slides
lineNumbers: false
fonts:
  sans: 'Nunito Sans'
  mono: 'Hack'
  fallbacks: false
  provider: none
addons:
  - slidev-addon-qrcode
  - fancy-arrow
background: /img/bg.jpg
monaco: false
---

# Porting the TypeScript Compiler to Go

<h2 id="cover-subtitle">for a 10x Speedup 🚀</h2>

<br>
<br>
<br>
<br>
<br>
<br>

## Jake Bailey

#### TypeScript @ Microsoft

<br>
<br>
<br>

<img src="/img/gophercon-logo-round.png" alt="GopherCon 2025 logo" id="gophercon-logo" />

<img src="/img/me.jpg" alt="Professional headshot of Jake Bailey, a man with brown hair and beard wearing an olive green t-shirt, photographed outdoors by a body of water at sunset" id="profile-pic" />

<style>
  h1 {
    font-size: 3rem !important;
    /* margin-bottom: 0 !important; */
  }
  #cover-subtitle {
    font-size: 2rem;
    font-style: italic;
    opacity: 0.5;
  }
  #gophercon-logo {
    position: absolute;
    top: 55%;
    right: 5%;
    width: 20%;
    box-shadow: none;
    border-radius: 0px;
  }
  #profile-pic {
    position: absolute;
    top: 60%;
    left: 30%;
    width: 10%;
    border-radius: 50%;
    object-fit: cover;
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
  }
</style>

<!--
Welcome, everyone! I'm Jake, I work on the TypeScript team at Microsoft.

It's been a long day of great talks; thanks for sticking around for one more!

Let's get right into it!
-->

---
layout: section
---

# What is TypeScript?

---

# What is TypeScript?

## 

JavaScript<span v-click.at="+1">, with types!</span>

````md magic-move {lines: false}
```js
function add(a, b) {
    return a + b;
}

const obj = { width: 10, height: 15 };
const area = obj.width * obj.heigth;

let id;
console.log(document.getElementById(id));
```

```ts
function add(a: number, b: number): number {
    return a + b;
}

const obj = { width: 10, height: 15 };
const area = obj.width * obj.heigth;

let id: string | undefined;
console.log(document.getElementById(id));
```
````

<!--
In short, it's JavaScript

With Types!

TypeScript is a superset of JavaScript, with a rich type system and toolchain.
 -->

---

# What is TypeScript?

## 

JavaScript, with types! And errors!

```ts twoslash
function add(a: number, b: number): number {
    return a + b;
}

const obj = { width: 10, height: 15 };
const area = obj.width * obj.heigth;

let id: string | undefined;
console.log(document.getElementById(id));
```

<!--
TypeScript uses the types you declare to find bugs before running your JavaScript.
-->

---

# What is TypeScript?

## 

<!-- dprint-ignore-start -->
```ts
type Status = "pending" | "success" | "error"; // Union types

type UUID = `${string}-${string}-${string}-${string}-${string}`; // String template types

interface ApiResponse<T> { // Generics
    data: T;
    status: Status;
    id?: UUID | undefined;
};

type IsString<T> = T extends string ? true : false; // Conditional types

type ReadonlyUser<T> = { // Mapped types
  readonly [K in keyof T]: T[K];
};
```
<!-- dprint-ignore-end -->

<!--
TypeScript has lots of goodies; generics, union types, conditional types, mapped types, and more.

None of which I'm going to talk about today!
 -->

---

# But, it's still just JavaScript!

## 

<!-- dprint-ignore-start -->
````md magic-move {lines: false}
```ts
class Person {
    name: string;
    #friends = new Set<Person>();
    constructor(name: string) {
        this.name = name;
    }
}

interface Named { readonly name: string; }

type Partial<T> = { [P in keyof T]?: T[P]; };

function greet(user: Partial<Named> | undefined) {
    console.log(`Hello, ${user?.name ?? "stranger"}`);
}
```

```js
class Person {
    name;
    friends = new Set();
    constructor(name) {
        this.name = name;
    }
}

function greet(user) {
    console.log(`Hello, ${user?.name ?? "stranger"}`);
}
```
````
<!-- dprint-ignore-end -->

<!--
But again, TypeScript is just JavaScript!

What TypeScript does is take TypeScript code, verifies it, and then
writes it out as plain JavaScript to be executed in places like Node.js or browsers.
-->

---

<img src="/img/ts2012.png" alt="Wayback machine of TypeScript's website in 2012" />

<style>
	img {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		max-width: 80%;
		max-height: 80%;
		object-fit: contain;
	}
</style>

<!--
TypeScript launched back in 2012, with the promise of allowing for the
development of application-scale JavaScript codebases.

Before us, writing JavaScript at scale was pretty rough to say the least.
-->

---

<img src="/img/ms-github.png" alt="Wayback machine of Microsoft's GitHub page in 2014, it's just TypeScript" />

<style>
	img {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		max-width: 80%;
		max-height: 80%;
		object-fit: contain;
	}
</style>

<!--
It was also the first project on Microsoft's GitHub org back in 2014.
-->

---

<img src="/img/GitHub-Octoverse-2024-top-programming-languages.png" alt="Graph from GitHub's Octoverse 2024 report showing the top programming languages from 2014-2024. In 2024, the top languages include Python (1), JavaScript (2), TypeScript (3), Java (4), C# (5), C++ (6), PHP (7), Shell (8), C (9), and Go (10)." class="main"  />

[github.blog/news-insights/octoverse/octoverse-2024/](https://github.blog/news-insights/octoverse/octoverse-2024/)

<style>
  img.main {
    height: 95%;
    margin-left: auto;
    margin-right: auto;
  }
  p {
    text-align: right;
  }
</style>

<!--
Since then, TS has grown more than we could imagine, becoming one of the most popular languages out there.

Currently it's at number three on GitHub, behind Python and JavaScript itself.

Last year, Python beat out JS, but TS and JS together are the biggest.

And JavaScript losing second place is probably our fault, because...
-->

---

# Most JavaScript devs are actually TypeScript devs

## 

_"How do you divide your time between writing JavaScript and TypeScript code?"_
-- [State of JS 2024](https://2024.stateofjs.com/en-US/usage/#js_ts_balance)

![State of JS 2024 survey results, average 74% TS usage, only 8% say no TS](/img/ts-usage.png)

<!--
Most JavaScript devs are actually TypeScript devs.

Last year's State of JS survey asked thousands how much time they spent between JS and TS,
and only 8% of respondents said they didn't use TypeScript at all.

But the thing is, all JavaScript devs are TypeScript devs too, because...
-->

---

# Most JavaScript devs are actually TypeScript devs

## 

_Even if they don't know it!_

<!-- dprint-ignore-start -->
<div class="monaco-editor-container">
  <div class="monaco-editor" data-theme="vs-dark">
    <div class="monaco-editor-background">
      <div class="view-lines">
        <div class="view-line" style="top:10px;height:19px;">
          <span class="mtk6">const</span><span class="mtk1">&nbsp;</span><span class="mtk12">myCats</span><span class="mtk1">&nbsp;</span><span class="mtk9">=</span><span class="mtk1">&nbsp;</span><span class="mtk6">new</span><span class="mtk1">&nbsp;</span><span class="mtk3">Set</span><span class="mtk1">(</span><span class="mtk1">[</span><span class="mtk17">"Nori"</span><span class="mtk1">,&nbsp;</span><span class="mtk17">"Miso"</span><span class="mtk1">,&nbsp;</span><span class="mtk17">"Momo"</span><span class="mtk1">]</span><span class="mtk1">)</span>
        </div>
        <div class="view-line" style="top:29px;height:19px;">
          <span class="mtk12">myCats</span><span class="mtk1">.</span><span class="mtk3">add</span><span class="mtk1">(</span><span class="mtk17">"???"</span><span class="mtk1">)</span>
        </div>
        <div class="view-line" style="top:48px;height:19px;"></div>
        <div class="view-line" style="top:67px;height:19px;"></div>
        <div class="view-line" style="top:86px;height:19px;">
          <span class="mtk12">document</span><span class="mtk1">.</span><span class="mtk4">getE</span><span class="cursor">|</span>
        </div>
        <div class="view-line" style="top:105px;height:19px;"></div>
        <div class="view-line" style="top:124px;height:19px;"></div>
        <div class="view-line" style="top:143px;height:19px;"></div>
        <div class="view-line" style="top:162px;height:19px;"></div>
        <div class="view-line" style="top:181px;height:19px;"></div>
        <div class="view-line" style="top:200px;height:19px;"></div>
        <div class="view-line" style="top:219px;height:19px;"></div>
        <div class="view-line" style="top:238px;height:19px;">
          <span class="mtk4">func</span><span class="mtk1">&nbsp;</span><span class="mtk3">whatsMyLanguageAgain</span><span class="mtk1">(</span><span class="mtk1">)</span><span class="mtk1">&nbsp;</span><span class="mtk1">{</span>
        </div>
        <div class="view-line" style="top:257px;height:19px;">
          <span class="mtk1">&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="mtk6">return</span><span class="mtk1">&nbsp;</span><span class="mtk8">182</span>
        </div>
        <div class="view-line" style="top:276px;height:19px;">
          <span class="mtk1">}</span>
        </div>
      </div>
      <div class="view-overlays">
        <div class="cdr squiggly-error" style="position:absolute;top:115px;left:98px;width:31px;height:2px;"></div>
        <div class="cdr squiggly-error" style="position:absolute;top:267px;left:22px;width:31px;height:2px;"></div>
      </div>
    </div>
  </div>
  <!-- Hover tooltip for myCats -->
  <div v-click="1" class="monaco-hover" style="top: 40px; left: 120px;">
    <div class="monaco-hover-content">
      <div class="hover-text">(variable) myCats: Set&lt;string&gt;</div>
    </div>
  </div>
  <!-- Completion popup -->
  <div v-click="2" class="suggest-widget" style="top: 115px; left: 130px;">
    <div class="suggest-list">
      <div class="suggest-item suggest-item-selected">
        <span class="suggest-icon codicon codicon-symbol-method"></span>
        <span class="suggest-label">getElementById</span>
        <span class="suggest-type">HTMLElement | null</span>
      </div>
      <div class="suggest-item">
        <span class="suggest-icon codicon codicon-symbol-method"></span>
        <span class="suggest-label">getElementsByClassName</span>
        <span class="suggest-type">HTMLCollection</span>
      </div>
      <div class="suggest-item">
        <span class="suggest-icon codicon codicon-symbol-method"></span>
        <span class="suggest-label">getElementsByTagName</span>
        <span class="suggest-type">HTMLCollection</span>
      </div>
    </div>
  </div>
  <!-- Error tooltip for 'func' -->
  <div v-click="3" class="monaco-hover error-hover" style="top: 205px; left: 20px;">
    <div class="monaco-hover-content">
      <div class="error-text">
        <span class="error-code">TS1003:</span> Identifier expected.
      </div>
    </div>
  </div>
</div>

<style>
.monaco-editor-container {
  position: relative;
  width: 100%;
  min-height: 320px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0,0,0,0.3);
}

.monaco-editor {
  position: relative;
  font-family: var(--slidev-code-font-family), 'Droid Sans Mono', 'monospace', monospace;
  font-size: 14px;
  line-height: 19px;
  width: 100%;
  height: 320px;
}

.monaco-editor-background {
  position: absolute;
  width: 100%;
  height: 100%;
  padding: 10px 20px;
}

.view-lines {
  position: relative;
  width: 100%;
  height: 100%;
}

.view-line {
  position: absolute;
  width: 100%;
  white-space: pre;
}

.view-overlays {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.cdr.squiggly-error {
  position: absolute;
  bottom: 0;
  height: 2px;
  background-image: url("data:image/svg+xml,%3csvg width='6' height='3' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='m0 3 l2 -2 l1 0 l2 2 l1 0' stroke='%23f14c4c' fill='none' stroke-width='1'/%3e%3c/svg%3e");
  background-repeat: repeat-x;
  background-position: bottom;
}

.cursor {
  animation: blink 1s infinite;
  font-weight: normal;
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}

/* Monaco Token Colors - Dark Theme */
.monaco-editor[data-theme="vs-dark"] {
  background-color: #1e1e1e;
  color: #d4d4d4;
}

.monaco-editor[data-theme="vs-dark"] .monaco-editor-background {
  background-color: #1e1e1e;
}

.monaco-editor[data-theme="vs-dark"] .mtk1 { color: #d4d4d4; } /* default/punctuation */
.monaco-editor[data-theme="vs-dark"] .mtk3 { color: #4ec9b0; } /* types/functions */
.monaco-editor[data-theme="vs-dark"] .mtk4 { color: #f14c4c; } /* errors */
.monaco-editor[data-theme="vs-dark"] .mtk6 { color: #569cd6; } /* keywords */
.monaco-editor[data-theme="vs-dark"] .mtk8 { color: #b5cea8; } /* numbers */
.monaco-editor[data-theme="vs-dark"] .mtk9 { color: #d4d4d4; } /* operators */
.monaco-editor[data-theme="vs-dark"] .mtk12 { color: #9cdcfe; } /* variables */
.monaco-editor[data-theme="vs-dark"] .mtk17 { color: #ce9178; } /* strings */

/* Monaco Token Colors - Light Theme */
.monaco-editor[data-theme="vs"] {
  background-color: #ffffff;
  color: #000000;
}

.monaco-editor[data-theme="vs"] .monaco-editor-background {
  background-color: #ffffff;
}

.monaco-editor[data-theme="vs"] .mtk1 { color: #000000; } /* default/punctuation */
.monaco-editor[data-theme="vs"] .mtk3 { color: #267f99; } /* types/functions */
.monaco-editor[data-theme="vs"] .mtk4 { color: #cd3131; } /* errors */
.monaco-editor[data-theme="vs"] .mtk6 { color: #0000ff; } /* keywords */
.monaco-editor[data-theme="vs"] .mtk8 { color: #098658; } /* numbers */
.monaco-editor[data-theme="vs"] .mtk9 { color: #000000; } /* operators */
.monaco-editor[data-theme="vs"] .mtk12 { color: #001080; } /* variables */
.monaco-editor[data-theme="vs"] .mtk17 { color: #a31515; } /* strings */

/* Theme switching based on Slidev's dark mode */
html:not(.dark) .monaco-editor {
  background-color: #ffffff;
  color: #000000;
}

html:not(.dark) .monaco-editor .monaco-editor-background {
  background-color: #ffffff;
}

html:not(.dark) .monaco-editor .mtk1 { color: #000000; }
html:not(.dark) .monaco-editor .mtk3 { color: #267f99; }
html:not(.dark) .monaco-editor .mtk4 { color: #cd3131; }
html:not(.dark) .monaco-editor .mtk6 { color: #0000ff; }
html:not(.dark) .monaco-editor .mtk8 { color: #098658; }
html:not(.dark) .monaco-editor .mtk9 { color: #000000; }
html:not(.dark) .monaco-editor .mtk12 { color: #001080; }
html:not(.dark) .monaco-editor .mtk17 { color: #a31515; }

html.dark .monaco-editor {
  background-color: #1e1e1e;
  color: #d4d4d4;
}

html.dark .monaco-editor .monaco-editor-background {
  background-color: #1e1e1e;
}

html.dark .monaco-editor .mtk1 { color: #d4d4d4; }
html.dark .monaco-editor .mtk3 { color: #4ec9b0; }
html.dark .monaco-editor .mtk4 { color: #f14c4c; }
html.dark .monaco-editor .mtk6 { color: #569cd6; }
html.dark .monaco-editor .mtk8 { color: #b5cea8; }
html.dark .monaco-editor .mtk9 { color: #d4d4d4; }
html.dark .monaco-editor .mtk12 { color: #9cdcfe; }
html.dark .monaco-editor .mtk17 { color: #ce9178; }

/* Monaco Hover */
.monaco-hover {
  position: absolute;
  z-index: 100;
  border-radius: 3px;
  animation: fadeIn 0.15s ease-out;
  line-height: 0.8rem;
}

.monaco-hover-content {
  padding: 6px 8px;
  font-size: 13px;
  max-width: 500px;
}

/* Dark theme hover */
html.dark .monaco-hover {
  background-color: #252526;
  border: 1px solid #454545;
  box-shadow: 0 2px 8px rgba(0,0,0,0.32);
}

html.dark .monaco-hover .hover-text {
  color: #cccccc;
}

html.dark .monaco-hover.error-hover {
  background-color: #3c1e1e;
  border-color: #be1100;
}

html.dark .monaco-hover.error-hover .error-text {
  color: #f14c4c;
}

/* Light theme hover */
html:not(.dark) .monaco-hover {
  background-color: #f8f8f8;
  border: 1px solid #c8c8c8;
  box-shadow: 0 2px 8px rgba(0,0,0,0.16);
}

html:not(.dark) .monaco-hover .hover-text {
  color: #1e1e1e;
}

html:not(.dark) .monaco-hover.error-hover {
  background-color: #f2dede;
  border-color: #cd3131;
}

html:not(.dark) .monaco-hover.error-hover .error-text {
  color: #cd3131;
}

.error-code {
  font-weight: 600;
}

/* Suggest Widget (Completion) */
.suggest-widget {
  position: absolute;
  z-index: 100;
  border-radius: 3px;
  animation: fadeIn 0.15s ease-out;
  min-width: 300px;
}

.suggest-list {
  max-height: 200px;
  overflow: hidden;
}

.suggest-item {
  display: flex;
  align-items: center;
  padding: 2px 0;
  cursor: pointer;
  height: 22px;
  padding: 0 8px;
}

.suggest-item-selected {
  background-color: var(--vscode-list-activeSelectionBackground, #0e639c);
}

.suggest-icon {
  width: 16px;
  height: 16px;
  margin-right: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 11px;
  border-radius: 2px;
  color: white;
  background-color: #652d90;
}

.suggest-label {
  flex: 1;
  font-size: 13px;
  line-height: 22px;
  margin-right: 8px;
}

.suggest-type {
  font-size: 11px;
  opacity: 0.7;
}

/* Dark theme suggest widget */
html.dark .suggest-widget {
  background-color: #252526;
  border: 1px solid #454545;
  box-shadow: 0 2px 8px rgba(0,0,0,0.32);
}

html.dark .suggest-item {
  color: #cccccc;
}

html.dark .suggest-item:hover:not(.suggest-item-selected) {
  background-color: #2a2d2e;
}

html.dark .suggest-item-selected {
  background-color: #094771;
  color: white;
}

/* Light theme suggest widget */
html:not(.dark) .suggest-widget {
  background-color: #f8f8f8;
  border: 1px solid #c8c8c8;
  box-shadow: 0 2px 8px rgba(0,0,0,0.16);
}

html:not(.dark) .suggest-item {
  color: #1e1e1e;
}

html:not(.dark) .suggest-item:hover:not(.suggest-item-selected) {
  background-color: #f0f0f0;
}

html:not(.dark) .suggest-item-selected {
  background-color: #0078d4;
  color: white;
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-4px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.slidev-vclick-target {
  transition: all 300ms ease;
}

.slidev-vclick-hidden {
  opacity: 0;
  transform: translateY(-8px);
}
</style>
<!-- dprint-ignore-end -->

<!--
TypeScript powers JS support in most editors.

Hovers? That's us.

Completions? That's us too.

Syntax errors? Yep, that's us too. Even in untyped JavaScript files.

The TypeScript toolchain and
types makes all of the features work, be it in  TypeScript or JavaScript.
 -->

---

# TypeScript is written in TypeScript

## 

<br>

<LightOrDark>
  <template #dark="props">
    <img src="/img/ts-repo-dark.png" v-bind="props" class="main" alt="GitHub repository page for microsoft/TypeScript showing file structure with folders like .devcontainer, .github, .vscode, bin, scripts, src, tests and various configuration files, along with recent commit information and contributor statistics" />
  </template>
  <template #light="props">
    <img src="/img/ts-repo-light.png" v-bind="props" class="main" alt="GitHub repository page for microsoft/TypeScript showing file structure with folders like .devcontainer, .github, .vscode, bin, scripts, src, tests and various configuration files, along with recent commit information and contributor statistics" />
  </template>
</LightOrDark>

<LightOrDark>
  <template #dark="props">
    <img src="/img/ts-repo-dark.png" v-bind="props" class="zoom" alt="Close-up view of the TypeScript repository's language statistics bar showing 99.9% TypeScript with a small portion of other languages" />
  </template>
  <template #light="props">
    <img src="/img/ts-repo-light.png" v-bind="props" class="zoom" alt="Close-up view of the TypeScript repository's language statistics bar showing 99.9% TypeScript with a small portion of other languages" />
  </template>
</LightOrDark>

<style>
img.main {
  height: 80%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 4%;
}
img.zoom {
  position: absolute;
  left: 50%;
  top: 60%;
  height: 70px;
  width: 400px;
  object-fit: none;
  object-position: 80.6% 84.8%;
  /* border: 2px solid #888; */
}
</style>

<!--
Now, like most languages, TypeScript is written in TypeScript.
That itself is not unusual -- most languages are written in themselves --,
but since TypeScript is just JavaScript,
what's unusual is having a _compiler_ written in JavaScript.

There's a tremendous benefit to being self-hosted.

We get immediate feedback from our own code.

If something is buggy in the language or the editor support, we go fix it.

The TypeScript community knows TypeScript, and can send us fixes.
 -->

---

# But, challenges...

<v-clicks depth="2">

- JavaScript wasn't designed for _writing compilers_ 🙃
  - Design constraints are suited for the browser / DOM, sandboxes
  - Inherent language overheads; e.g. expensive object model
  - You can't share objects between threads
  - `async`/`await` means function coloring; non-zero cost of `Promise`
  - 4GB memory limit in many builds of Node.js (e.g. Electron → VS Code)
- We squeezed as much out of it as we could
  - Loads of profiling, caching, "monomorphization"
  - Still, performance woes, OOMs 😢

</v-clicks>

<!--
So, there were of course challenges.

- JavaScript wasn't designed for _writing compilers_.
  - The language is more designed for the browser or sandboxes
  - As efficient as modern JS runtimes are, there are still inherent overheads
  - You can't share objects between threads, so if you want to do multithreading,
    you need to serialize, defeating the purpose much of the time.
  - `async`/`await`/`Promise` means function coloring; non-zero cost of actually
    creating Promises all the time
  - And many builds of JavaScript have a memory limit; including the runtime
    that's bundled with VS Code.
- We squeezed as much out of it as we could
  - Loads of profiling, caching, "monomorphization"
  - Still, performance woes, OOMs 😢
  - People have massive codebases only getting larger

Now, to be clear JavaScript is always improving,
but even if we get some of this fixed,
it'll be a long time before we're able to use it.
-->

---
layout: section
---

# Can we rewrite TypeScript in another language?

<!--
Now, last fall, we started asking ourselves the question everyone had been asking us forever.

Could we rewrite the TypeScript compiler in another language?

We said no for a long time, kept working to squeeze more out of JS.
But, we were hitting enough walls to try and prototype something.
-->

---

<div class="choice-row">
  <img src="/img/rust-logo-512x512.png" alt="Rust programming language logo" style="filter: brightness(1.75);" />
  <img src="/img/Go-Logo_Blue.svg" alt="Go programming language logo" />
  <img src="/img/Logo_C_sharp.svg" alt="C# programming language logo" />
  <img src="/img/zig-mark.svg" alt="Zig programming language logo" />
  <img src="/img/OCaml_Sticker.svg" alt="OCaml programming language logo" />
  <span class="choice-more">. . . ?</span>
</div>

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

<p style="text-align: right; opacity: 0.2; font-size: 0.5rem">
<a href="https://github.com/rust-lang/rust-artwork/blob/master/logo/rust-logo-512x512.png">Rust logo</a> by ™/®Rust Foundation / <a href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>,
<a href="https://github.com/ziglang/logo/blob/master/zig-mark.svg">Zig logo</a> by KeyboardRage / <a href="https://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a>,
</p>

<style>
  .choice-row {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(2, 1fr);
    justify-items: center;
    align-items: center;
    gap: 15px;
    width: 60%;
  }
  .choice-row img {
    height: 120px;
    width: auto;
    object-fit: contain;
    box-shadow: none;
    border-radius: 0px;
  }
  .choice-more {
    font-size: 3rem;
    font-weight: bold;
    margin-left: 20px;
  }
</style>

<!--
Obviously, many options out there.

Good reasons and precedent for any of these (and more).

Rust is popular; trend of rewriting in Rust, many JS tools are in Rust or use Rust.

Go has precedence via esbuild, the pioneer of JS tools written in a compiled language.

One of the newer JS runtimes is written in Zig, and Flow's compiler is written in OCaml.

Obviously there's C#, which has heavy investment at Microsoft; it's cross-platform, fast, has Node.js bindings.
-->

---

# Requirements

## 

<v-clicks>

- Fast (duh!)
  - Compiles to native code
  - Strong support for shared memory concurrency
- Multi-platform
  - Including WebAssembly for browsers

</v-clicks>

<v-clicks>

_But what else?_

</v-clicks>

<!--
Let's think about some of the requirements we have.

Obviously, if we're going to rewrite in another language, that language
has to be fast. We want to compile to native code, and we want support
for shared memory concurrency and multi-threading so we can actually
make use of all of the cores on a system.

We also want to ensure we can build cross-platform, since before we were
able to run anywhere JavaScript runs.

But, there's another key gotcha here.
-->

---
layout: statement
---

# No spec!

<!--
TypeScript doesn't have a spec!  Many languages have specs,
many don't. TypeScript is one of the languages that only has a canonical implementation.
So the spec is whatever the 150 thousand lines of code in core compiler code do.

People depend on obscure behaviors, whether or not we even know we have them.

It's Hyrum's law but worse somehow.

Even if we had a spec, there still could be other behaviors that our users depend on.
For example, TypeScript has union types; sometimes the order matters, as much
as we try to ensure that it doesn't. Even in a spec, we'd probably make that ordering
undefined.
-->

---

<LightOrDark>
  <template #dark="props">
    <img src="/img/spec-dark.png" v-bind="props" class="main" alt="GitHub pull request #51791 titled 'Remove doc folder (old archived spec a
nd assets), word2md script' showing deleted files including TypeScript Language Specification documents, with +0 -7,242 lines changed" />
  </template>
  <template #light="props">
    <img src="/img/spec-light.png" v-bind="props" class="main" alt="GitHub pull request #51791 titled 'Remove doc folder (old archived spec and assets), word2md script' showing deleted files including TypeScript Language Specification documents, with +0 -7,242 lines changed"  />
  </template>
</LightOrDark>

<style>
	img {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		max-width: 80%;
		max-height: 80%;
		object-fit: contain;
	}
</style>

<!--
To be fair, there used to be a spec a long long time ago,
but it hadn't been updated in a very long time.

I deleted it after people kept trying to reference the spec even though it was out of date.
-->

---
layout: statement
---

## We can't rewrite.

# We have to _port_.

<!--

We can't rewrite the codebase, we need to port it.
It has to be fundamentally the same codebase, just in another language,
preserving as much of the original behavior as possible.

-->

---

# Requirements

## 

- Fast (duh)
  - Compile to native code
  - Strong support for shared memory concurrency
- Multi-platform
  - Including WebAssembly for browsers

<v-clicks depth="2">

- **_"Porting compatible"_**
  - **Structurally similar to TypeScript**
    - Tending away from OOP patterns, towards data / functions / interfaces
  - **Garbage collection**
    - Ergonomic cyclic data structures
  - **Easy to learn**

</v-clicks>

<!--
So, adding onto our list of requirements,we know that whatever we choose
must actually be possible to port into.


To start, to make this feasible, the chosen language must be structurally similar to TypeScript.
This also implies
a language that is less OOP and more data/functions/interfaces.

We need garbage collection. We allocate a lot of objects

We need the ability to have cycles in our
data structures. We have parent pointers in our ASTs. We have types that are recursive.
Manual memory management is a no-go.

It also needs to be easy to learn, to get everyone up to speed quickly
and actually finish the effort, and not be too complicated for external
contributors to pick up and contribute.

And so, all signs pointed to one language.
-->

---
layout: none
---

<img src="/img/Go-Logo_Blue.svg" alt="Go programming language logo" />

<style>
img {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 75%;
  width: auto;
  object-fit: contain;
  box-shadow: none;
  border-radius: 0px;
}
</style>

<!--
Go! Of course, you already knew that, we're here at GopherCon.
-->

---
layout: section
---

# To prototyping...

<!-- So let's go get to prototyping. -->

---

# Early prototyping

<v-clicks>

- Started hand-porting to Go from the bottom up, starting with the scanner and
  parser
- Meanwhile, a few of us futzed around with other languages, just to be sure 😅
- Parsing turned out to be **\~5x faster**!
- The handwritten code looked **extremely similar** to the original TypeScript

</v-clicks>

<!--
- Started from the bottom; hand porting the scanner and parser, the very base of our compiler.
- Meanwhile, a few of us futzed around with other languages, just to be sure
- Parsing turned out to be \~5x faster, without any optimizations! Just straight 1:1 exact same code.
- And the handwritten code looked extremely similar to the original TypeScript, proving that this might just be feasible.
-->

---

<!-- dprint-ignore-start -->
````md magic-move {lines: false}
```ts {*|2-4|6-9|10-14|*}
export function createTypeChecker(): TypeChecker {
    const unionTypes = new Map<string, UnionType>();
    const intersectionTypes = new Map<string, Type>();
    const anyType = createIntrinsicType(TypeFlags.Any, "any")
    // ...

    function getTypeAtLocation(location: Node): Type {/* ... */}
    function getApparentType(t: Type): Type {/* ... */}
    function getUnionSignatures(signatureLists: readonly (readonly Signature[])[]): Signature[] {/* ... */}

    return {
        getTypeAtLocation,
        getApparentType,
    };
}
```

```go {*}
type Checker struct {
    unionTypes         map[string, *UnionType]
    intersectionTypes  map[string, *Type]
    anyType            *Type
    // ...
}

func createTypeChecker() *Checker {
    c := &Checker{}
    c.unionTypes = make(map[string]*UnionType)
    c.intersectionTypes = make(map[string]*Type)
    c.anyType = c.createIntrinsicType(TypeFlagsAny, "any")
    // ...
    return c
}

func (c *Checker) getTypeAtLocation(location *Node) *Type {/* ... */}
func (c *Checker) getApparentType(t *Type) *Type {/* ... */}
func (c *Checker) getUnionSignatures(signatureLists [][]*Signature) []*Signature {/* ... */}
```
````
<!-- dprint-ignore-end -->

<!--
So to get a rough idea of what porting looked like, let's look at an example.

Our old code was effectively class-free.

Functions close over state, inner functions do the work, we return to export an API. Strangely enough, this is the fastest way to do it in JavaScript.

In Go, we can more simply write plain structs and methods.
We don't need the inheritance or polymorphism, just data and functions.
-->

---

<LightOrDark>
  <template #dark="props">
    <img src="/img/ts-to-go-dark.png" v-bind="props" class="main" alt="GitHub repository page for jakebailey/ts-to-go showing file structure with folders like .vscode, output, and files like .dprint.jsonc, LICENSE, README.md, with 'Very hacky transformer from TS to Go' description and language breakdown showing 89.8% Go, 9.6% TypeScript, 0.6% JavaScript" />
  </template>
  <template #light="props">
    <img src="/img/ts-to-go-light.png" v-bind="props" class="main" alt="GitHub repository page for jakebailey/ts-to-go showing file structure with folders like .vscode, output, and files like .dprint.jsonc, LICENSE, README.md, with 'Very hacky transformer from TS to Go' description and language breakdown showing 89.8% Go, 9.6% TypeScript, 0.6% JavaScript" />
  </template>
</LightOrDark>

<div id="ts-to-go-link">

[github.com/jakebailey/ts-to-go](https://github.com/jakebailey/ts-to-go)

</div>

<style>
	img.main {
  height: 90%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 4%;
}
	a {
		position: absolute;
		bottom: 150px;
		right: 50px;
	}
	#ts-to-go-link {
		position: absolute;
		bottom: 120px;
		right: 50px;
		background-color: #007aff;
		border: 2px solid #007aff;
		border-radius: 8px;
		padding: 8px 12px;
	}
	#ts-to-go-link a {
		position: static;
		color: white;
		text-decoration: none;
	}
</style>

<!--
And so early on while the scanner/parser were being ported, I wrote a tool
that loosely transforms TypeScript code into Go code.

ts-to-go uses TypeScript's API to parse out our own compiler,
then converts TS syntax in to Go, using type information to write
down types where needed.
-->

---

<!-- dprint-ignore-start -->
````md magic-move {lines: false}
```ts
function bindForStatement(node: ForStatement): void {
    const preLoopLabel = setContinueTarget(node, createLoopLabel());
    const preBodyLabel = createBranchLabel();
    const postLoopLabel = createBranchLabel();
    bind(node.initializer);
    addAntecedent(preLoopLabel, currentFlow);
    currentFlow = preLoopLabel;
    bindCondition(node.condition, preBodyLabel, postLoopLabel);
    currentFlow = finishFlowLabel(preBodyLabel);
    bindIterativeStatement(node.statement, postLoopLabel, preLoopLabel);
    bind(node.incrementor);
    addAntecedent(preLoopLabel, currentFlow);
    currentFlow = finishFlowLabel(postLoopLabel);
}
```

```go
func (b *Binder) bindForStatement(node ForStatement) {
    preLoopLabel := b.setContinueTarget(node, b.createLoopLabel())
    preBodyLabel := b.createBranchLabel()
    postLoopLabel := b.createBranchLabel()
    b.bind(node.initializer)
    b.addAntecedent(preLoopLabel, b.currentFlow)
    b.currentFlow = preLoopLabel
    b.bindCondition(node.condition, preBodyLabel, postLoopLabel)
    b.currentFlow = b.finishFlowLabel(preBodyLabel)
    b.bindIterativeStatement(node.statement, postLoopLabel, preLoopLabel)
    b.bind(node.incrementor)
    b.addAntecedent(preLoopLabel, b.currentFlow)
    b.currentFlow = b.finishFlowLabel(postLoopLabel)
}
```
````
<!-- dprint-ignore-end -->

<!--

For example, some code that looks like this,

gets turned into this.
-->

---

<!-- dprint-ignore-start -->
````md magic-move {lines: false}
```ts
function getTypeOfSymbol(symbol: Symbol): Type {
    const checkFlags = getCheckFlags(symbol);
    if (checkFlags & CheckFlags.DeferredType) {
        return getTypeOfSymbolWithDeferredType(symbol);
    }
    if (checkFlags & CheckFlags.Instantiated) {
        return getTypeOfInstantiatedSymbol(symbol);
    }
    if (checkFlags & CheckFlags.Mapped) {
        return getTypeOfMappedSymbol(symbol as MappedSymbol);
    }
    if (checkFlags & CheckFlags.ReverseMapped) {
        return getTypeOfReverseMappedSymbol(symbol as ReverseMappedSymbol);
    }
    if (symbol.flags & (SymbolFlags.Variable | SymbolFlags.Property)) {
        return getTypeOfVariableOrParameterOrProperty(symbol);
    }
    // ...
    return errorType;
}
```

```go
func (c *Checker) getTypeOfSymbol(symbol *ast.Symbol) *Type {
    checkFlags := getCheckFlags(symbol)
    if checkFlags&ast.CheckFlagsDeferredType != 0 {
        return c.getTypeOfSymbolWithDeferredType(symbol)
    }
    if checkFlags&ast.CheckFlagsInstantiated != 0 {
        return c.getTypeOfInstantiatedSymbol(symbol)
    }
    if checkFlags&ast.CheckFlagsMapped != 0 {
        return c.getTypeOfMappedSymbol(symbol.(MappedSymbol))
    }
    if checkFlags&ast.CheckFlagsReverseMapped != 0 {
        return c.getTypeOfReverseMappedSymbol(symbol.(ReverseMappedSymbol))
    }
    if symbol.flags&(ast.SymbolFlagsVariable|ast.SymbolFlagsProperty) != 0 {
        return c.getTypeOfVariableOrParameterOrProperty(symbol)
    }
    // ...
    return c.errorType
}
```
````
<!-- dprint-ignore-end -->

<!--
Code that looks like this, with bitwise operations, type assertions, etc,

gets turned into this.
-->

---
layout: none
---

<img src="/img/same-picture.png" alt="The Office meme, 'Corporate needs you to find the differences between this picture and this picture. The two pictures are the same code in Go and TS.'" style="border-radius: 0px; transform: scale(1.02); object-fit: cover; object-position: center top;" />

<!--
Corporate needs you to find the differences between this picture and this picture.
-->

---

<!-- dprint-ignore-start -->
```ts {*|3}
function getPropertyNameFromBindingElement(e: BindingElement) {
	const exprType = getLiteralTypeFromPropertyName(
		e.propertyName || e.name as Identifier,
	);
	return isTypeUsableAsPropertyName(exprType)
		? getPropertyNameFromType(exprType)
		: undefined;
}
```

<br>


```go {*|2}{at:1}
func (c *Checker) getPropertyNameFromBindingElement(e BindingElement) *string {
	exprType := c.getLiteralTypeFromPropertyName(e.PropertyName || e.Name.AsIdentifier())
	if isTypeUsableAsPropertyName(exprType) {
		return getPropertyNameFromType(exprType)
	} else {
		return nil
	}
}
```
<!-- dprint-ignore-end -->

<!--
Now, it's not all a perfect one to one.

The output may be syntactically valid, but it is not necessarily going
to compile. Note the `||`, which in JavaScript means "take the left side if truthy,
otherwise the right side", which in Go would have to be an if statement.

So there's a bit of manual massaging that's required here.
-->

---

<!-- dprint-ignore-start -->
```ts {*|4-6|6}
function getApplicableIndexInfoForName(type: Type, name: __String): IndexInfo | undefined {
	return getApplicableIndexInfo(
		type,
		isLateBoundName(name)
			? esSymbolType
			: getStringLiteralType(unescapeLeadingUnderscores(name)),
	);
}
```

<br>

```go {*|4-8|7}{at:1}
func (c *Checker) getApplicableIndexInfoForName(t *Type, name string) *IndexInfo {
	return c.getApplicableIndexInfo(
		t,
		ifElse(
			c.isLateBoundName(name),
			c.esSymbolType,
			c.getStringLiteralType(unescapeLeadingUnderscores(name)),
		),
	)
}
```
<!-- dprint-ignore-end -->

<!--
Go also lacks a ternary operator, so that gets turned into a fake call
to an if else function.

Note that this is not necessarily a safe transformation; the call always
evaluates its arguments, so this else case would always run. This one also
requires some manual intervention.
-->

---

<!-- dprint-ignore-start -->
````md magic-move {lines: false}
```ts
function getApparentType(type: Type): Type {
	// ...
	return objectFlags & ObjectFlags.Mapped ? getApparentTypeOfMappedType(t as MappedType) :
		objectFlags & ObjectFlags.Reference && t !== type ? getTypeWithThisArgument(t, type) :
		t.flags & TypeFlags.Intersection ? getApparentTypeOfIntersectionType(t as IntersectionType, type) :
		t.flags & TypeFlags.StringLike ? globalStringType :
		t.flags & TypeFlags.NumberLike ? globalNumberType :
		// ...
		t.flags & TypeFlags.Unknown && !strictNullChecks ? emptyObjectType :
		t;
}
```

```go
func (c *Checker) getApparentType(type_ *Type) *Type {
	// ...
	switch {
	case objectFlags&ObjectFlagsMapped != 0:
		return c.getApparentTypeOfMappedType(t.AsMappedType())
	case objectFlags&ObjectFlagsReference != 0 && t != type_:
		return c.getTypeWithThisArgument(t, type_)
	case t.flags&TypeFlagsIntersection != 0:
		return c.getApparentTypeOfIntersectionType(t.AsIntersectionType(), type_)
	case t.flags&TypeFlagsStringLike != 0:
		return c.globalStringType
	case t.flags&TypeFlagsNumberLike != 0:
		return c.globalNumberType
	// ...
	case t.flags&TypeFlagsUnknown != 0 && !c.strictNullChecks:
		return c.emptyObjectType
	default:
		return t
	}
}
```
````
<!-- dprint-ignore-end -->

<!--
A pattern we used heavily in the old codebase were these sort of
"match case" nested ternary operator expressions. ts-to-go detects
these and turns them into switch cases. Maybe a little less concise,
but it is equivalent.
-->

---

# More progress

<v-clicks>

- With `ts-to-go` in hand, we started porting more and more code
  - Finished the binder, some of the checker
  - Perf continues to be great; 3-4x single threaded boost holds up
- Now, throw in concurrency, many projects compile **_10x faster_** 🚀
- At this point, the effort was undeniable

</v-clicks>

<!--
With ts-to-go in hand, we started porting more and more code.

Pretty soon the binder was done, some of the type checker.

Perf continues to be great.

Then, we added concurrency, which mind you, this is Go so that was
a couple of lines at most, and we're over 10x.

At this point, the benefit was undeniable.
-->

---

# Broadening the effort

## 

<v-clicks>

- Time to bring in the rest of the team
- \~10 engineers learning Go for the first time
  - Even some people who have only worked in TypeScript
  - But, the learning period was very short!
- Built a VFS, a basic CLI, basic file loading
- Each step unblocked the next
- To the point we're all working on editor support, tests, CLI, file watching,
  emit, and more
  - Concurrently 😉

</v-clicks>

<!--
It was time to broaden the effort and bring in the rest of the team.

We had about 10 engineers learning Go for the first time.

I was the only one who had written a meaningful amount of Go.

Some of us have only worked professionally in TypeScript.

But, the learning period was very short!
There was some teaching involved, but Go is a simple language.
Mainly advice about writing simpler straight line code, and not going
crazy with channels.

We built a virtual file system, a basic CLI, basic file loading.

Each step unblocked more work.

We got to the point where we were all working on editor support, tests, CLI,
file watching, emit, and more.
-->

---

# And pretty soon...

<div class="perf-chart">
  <div class="chart-header">
    <div class="project-label"></div>
    <div class="bar-labels">
      <span class="label-old">tsc (original)</span>
      <span class="label-new">tsgo (new)</span>
    </div>
  </div>

<div class="chart-row vscode">
    <div class="project-name">VS Code<br><span class="loc">1.5M LoC</span></div>
    <div class="bars">
      <div class="bar-old"><span class="time old-time"></span></div>
      <div class="bar-new-container">
        <div class="bar-new"><span class="time new-time"></span></div>
        <div class="speedup-indicator">
          <div class="bracket-line"></div>
          <div class="speedup-label"></div>
        </div>
      </div>
    </div>
  </div><div class="chart-row playwright">
    <div class="project-name">Playwright<br><span class="loc">356K LoC</span></div>
    <div class="bars">
      <div class="bar-old"><span class="time old-time"></span></div>
      <div class="bar-new-container">
        <div class="bar-new"><span class="time new-time"></span></div>
        <div class="speedup-indicator">
          <div class="bracket-line"></div>
          <div class="speedup-label"></div>
        </div>
      </div>
    </div>
  </div>

<div class="chart-row typeorm">
    <div class="project-name">TypeORM<br><span class="loc">270K LoC</span></div>
    <div class="bars">
      <div class="bar-old"><span class="time old-time"></span></div>
      <div class="bar-new-container">
        <div class="bar-new"><span class="time new-time"></span></div>
        <div class="speedup-indicator">
          <div class="bracket-line"></div>
          <div class="speedup-label"></div>
        </div>
      </div>
    </div>
  </div>

<div class="chart-row datefns">
    <div class="project-name">date-fns<br><span class="loc">104K LoC</span></div>
    <div class="bars">
      <div class="bar-old"><span class="time old-time"></span></div>
      <div class="bar-new-container">
        <div class="bar-new"><span class="time new-time"></span></div>
        <div class="speedup-indicator">
          <div class="bracket-line"></div>
          <div class="speedup-label"></div>
        </div>
      </div>
    </div>
  </div>

<div class="chart-row trpc">
    <div class="project-name">tRPC<br><span class="loc">18K LoC</span></div>
    <div class="bars">
      <div class="bar-old"><span class="time old-time"></span></div>
      <div class="bar-new-container">
        <div class="bar-new"><span class="time new-time"></span></div>
        <div class="speedup-indicator">
          <div class="bracket-line"></div>
          <div class="speedup-label"></div>
        </div>
      </div>
    </div>
  </div>

<div class="chart-row rxjs">
    <div class="project-name">RxJS<br><span class="loc">2.1K LoC</span></div>
    <div class="bars">
      <div class="bar-old"><span class="time old-time"></span></div>
      <div class="bar-new-container">
        <div class="bar-new"><span class="time new-time"></span></div>
        <div class="speedup-indicator">
          <div class="bracket-line"></div>
          <div class="speedup-label"></div>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .perf-chart {
    max-width: 900px;
    margin: 20px auto;
    font-family: var(--slidev-code-font-family);
  }

  .chart-header {
    display: flex;
    align-items: center;
    height: 30px;
  }

  .project-label {
    width: 140px;
  }

  .bar-labels {
    flex: 1;
    display: flex;
    gap: 20px;
    font-size: 14px;
    font-weight: bold;
  }

  .label-old {
    color: #ff9500;
  }

  .label-new {
    color: #007acc;
  }

  .chart-row {
    display: flex;
    align-items: center;
    margin-bottom: 6px;
    height: 50px;
  }

  .project-name {
    width: 140px;
    text-align: right;
    padding-right: 20px;
    font-weight: bold;
    font-size: 16px;
  }

  .loc {
    font-size: 12px;
    font-weight: normal;
    opacity: 0.7;
    display: block;
    margin-top: 2px;
  }

  .bars {
    flex: 1;
    position: relative;
    height: 50px;
  }

  .bar-old, .bar-new {
    height: 24px;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding-right: 10px;
    margin-bottom: 3px;
    min-width: 50px;
  }

  .bar-new-container {
    display: flex;
    height: 24px;
    margin-bottom: 3px;
    position: relative;
  }

  .bar-old {
    background: linear-gradient(90deg, #ffb347, #ff9500);
    opacity: 0.9;
  }

  .bar-new {
    background: linear-gradient(90deg, #4fc3f7, #007acc);
    margin-bottom: 0;
  }

  .time {
    color: white;
    font-weight: bold;
    font-size: 14px;
    text-shadow: 0 1px 2px rgba(0,0,0,0.5);
    white-space: nowrap;
  }

  .speedup-indicator {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    position: relative;
    margin-left: 10px;
    margin-right: 10px;
    border-bottom: 2px dashed #666;
    padding-right: 300px;
  }

  .speedup-indicator::before {
    content: '';
    position: absolute;
    left: 0;
    bottom: 0;
    width: 2px;
    height: 6px;
    border-left: 2px dashed #666;
  }

  .speedup-indicator::after {
    content: '';
    position: absolute;
    right: 0;
    bottom: 0;
    width: 2px;
    height: 6px;
    border-right: 2px dashed #666;
  }

  .bracket-line {
    display: none;
  }

  .speedup-label {
    font-size: 15px;
    font-weight: bold;
    color: var(--slidev-theme-primary);
    white-space: nowrap;
  }

  /* Project-specific styles */
  .vscode .bar-old { width: 100%; }
  .vscode .bar-new { width: calc(7.5 / 77.8 * 100%); }
  .vscode .old-time::after { content: "77.8s"; }
  .vscode .new-time::after { content: "7.5s"; }
  .vscode .speedup-label::after { content: "10.4x"; }

  .playwright .bar-old { width: 100%; }
  .playwright .bar-new { width: calc(1.1 / 11.1 * 100%); }
  .playwright .old-time::after { content: "11.1s"; }
  .playwright .new-time::after { content: "1.1s"; }
  .playwright .speedup-label::after { content: "10.1x"; }

  .typeorm .bar-old { width: 100%; }
  .typeorm .bar-new { width: calc(1.3 / 17.5 * 100%); }
  .typeorm .old-time::after { content: "17.5s"; }
  .typeorm .new-time::after { content: "1.3s"; }
  .typeorm .speedup-label::after { content: "13.5x"; }

  .datefns .bar-old { width: 100%; }
  .datefns .bar-new { width: calc(0.7 / 6.5 * 100%); }
  .datefns .old-time::after { content: "6.5s"; }
  .datefns .new-time::after { content: "0.7s"; }
  .datefns .speedup-label::after { content: "9.3x"; }

  .trpc .bar-old { width: 100%; }
  .trpc .bar-new { width: calc(0.6 / 5.5 * 100%); }
  .trpc .old-time::after { content: "5.5s"; }
  .trpc .new-time::after { content: "0.6s"; }
  .trpc .speedup-label::after { content: "9.2x"; }

  .rxjs .bar-old { width: 100%; }
  .rxjs .bar-new { width: calc(0.1 / 1.1 * 100%); }
  .rxjs .old-time::after { content: "1.1s"; }
  .rxjs .new-time::after { content: "0.1s"; }
  .rxjs .speedup-label::after { content: "11.0x"; }
</style>

<!--
Fast forward, and we've made enough progress to test on a
number of big projects. The performance boost held!

VS Code, a 1.5 million line codebase, previously took nearly 80 seconds
to compile on my pretty fast machine, and now took 7 seconds.

That same speedup applied even as the project size decreased.
-->

---
layout: section
---

## March 11th

# Finally, announcement day!

## [github.com/microsoft/typescript-go](https://github.com/microsoft/typescript-go)

<!--
Fast forward a few months.
VS Code is compiling cleanly.
We get everything looking good, and announce March 11th.
-->

---
layout: two-cols
---

<br>
<br>
<br>

<img src="/img/twitter.png" alt="Screenshot of a Twitter post showing the TypeScript to Go announcement receiving significant engagement and discussion" />

::right::

<div class="image-overlay">
  <img src="/img/yt1.jpg" alt="YouTube thumbnail from The Code Report channel titled 'TS 10x faster...' featuring the TypeScript logo and a dramatic image from the movie Prometheus of a character looking upward with blue-tinted lighting" v-if="0 < $clicks"
       v-motion
       :initial="{ x: -300, y: -400, rotate: -45 }"
       :enter="{ x: -80, y: -40, rotate: -2, transition: { duration: 600, ease: 'easeOut' } }" />
  <img v-click src="/img/yt2.jpg" alt="YouTube thumbnail featuring Anders Hejlsberg (TypeScript lead architect) with text '½ the memory | 10x faster | concurrent' and 'TS → GO', showing the transition from TypeScript to Go with a photo of Anders smiling" v-if="1 < $clicks"
       v-motion
       :initial="{ x: 400, y: -150, rotate: 60 }"
       :enter="{ x: 90, y: -20, rotate: 3, transition: { duration: 700, ease: 'easeOut' } }" />
  <img v-click src="/img/yt3.jpg" alt="YouTube thumbnail showing TypeScript logo with arrow pointing to the Go gopher mascot, while the Rust game logo (not the programming language) has a sad emoji. Features a person doing a facepalm gesture at a microphone, humorously reacting to the language choice" v-if="2 < $clicks"
       v-motion
       :initial="{ x: -250, y: 600, rotate: -30 }"
       :enter="{ x: -60, y: 60, rotate: -1, transition: { duration: 650, ease: 'easeOut' } }" />
  <img v-click src="/img/yt4.png" alt="YouTube video from official TypeScript account (@typescript) titled 'We're porting to Go' posted March 11, 2025 at 7:37 AM with 203K views. Shows video by Theo-t3.gg titled 'TypeScript just changed forever' with 283K views from 5 months ago" v-if="3 < $clicks"
       v-motion
       :initial="{ x: 350, y: 250, rotate: 90 }"
       :enter="{ x: 70, y: 80, rotate: 2, transition: { duration: 750, ease: 'easeOut' } }" />
</div>

<!-- Hack: make clicks extend to the right count. -->

<span v-click="4"></span>

<style>
.image-overlay {
  height: 400px;
}

.image-overlay img {
  position: absolute;
  top: 27%;
  left: 60%;
  width: 280px;
  height: auto;
  object-fit: cover;
  transform: translate(-50%, -50%);
}
</style>

<!--
Reception was overwhelming.

Most people were flabbergasted.

The YouTubers were eating it up.

CLICK WHILE TALKING
-->

---
layout: statement
---

# Why not rewrite it in ﹏﹏﹏?

## Obviously you should have rewritten in ﹏﹏﹏\!\!

### Why didn't you rewrite it in ﹏﹏﹏?\!??

#### Why aren't you switching to ﹏﹏﹏?\!\!?\!\!\!\!\!\!\!

#### Why not ﹏﹏﹏\?\!?\!?\!?\!

##### 🫠

<!--
Of course, as we expected, most questions were why we didn't rewrite it in
Rust, or C#, or Zig, and so on.

Lots of Reddit, HackerNews, Twitter, Bluesky threads.

Even comments on our release blog, the very blog where we explained why we did it!

But thankfully, some people in our community understood what really mattered.
-->

---
layout: two-cols
---

<img src="/img/doom.png" alt="Twitter/X post by Seb from ThisWeekInReact.com showing announcement 'All this so that we can play Doom with decent FPS 😏' with Michigan TypeScript's tweet about 'Doom now runs in @typescript types. What a journey this one's been.' featuring the classic Doom game logo stylized as 'TYPESCRIPT' with the iconic Doom marine character in a hellish red landscape" />

::right::

<img src="/img/doom2.png" alt="Twitter/X conversation where Andrew Allen asks 'can it run doom?' and Samuel replies 'yeah' with a link to YouTube video 'TypeScript types can run DOOM' by Michigan TypeScript, featuring the same Doom logo styled as 'TYPESCRIPT' with the iconic Doom marine character" />

<style>
  img {
    height: 90%;
    margin: 0 auto;
  }
</style>

<!--
Could our turing complete type system still run DOOM?
-->

---
layout: section
---

# The Go community

<!--
The excitement didn't limit itself to the TypeScript community.
The gophers were excited too!
-->

---

<LightOrDark>
	<template #dark="props">
	<img src="/img/escape-issue-dark.png" alt="GitHub issue #72815 showing slow escape analysis in Go compiler when compiling TypeScript, with benchmark results and CPU profile highlighting escape analysis performance bottlenecks" class="main" />
		<img v-click src="/img/escape-issue-dark.png" alt="GitHub issue #72815 showing slow escape analysis in Go compiler when compiling TypeScript, with benchmark results and CPU profile highlighting escape analysis performance bottlenecks" class="zoom-dark" />
	</template>
	<template #light="props">
		<img src="/img/escape-issue-light.png" alt="GitHub issue #72815 showing slow escape analysis in Go compiler when compiling TypeScript, with benchmark results and CPU profile highlighting escape analysis performance bottlenecks" class="main" />
		<img v-click src="/img/escape-issue-light.png" alt="GitHub issue #72815 showing slow escape analysis in Go compiler when compiling TypeScript, with benchmark results and CPU profile highlighting escape analysis performance bottlenecks" class="zoom-light" />
	</template>
</LightOrDark>

<style>
  img.main {
    height: 100%;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 4%;
  }
  img.zoom-light {
    position: absolute;
    left: 20%;
    top: 20%;
    height: 70px;
    width: 200px;
    object-fit: none;
    object-position: 12.8% 22%;
    border: 2px solid #888;
  }
  img.zoom-dark {
    position: absolute;
    left: 20%;
    top: 20%;
    height: 70px;
    width: 230px;
    object-fit: none;
    object-position: 12.6% 23%;
    border: 2px solid #888;
  }
</style>

<!--
Right away, Go contributors were testing out our code.

CLICK

On the same day we announced, someone filed a bug about the Go compiler
being slow when compiling the TypeScript compiler!
-->

---
layout: none
---

<LightOrDark>
	<template #dark="props">
		<img src="/img/sweet-dark.png" alt="Go code review showing merged change #657077 'sweet: add typescript-go to go-build benchmark' with approval status and review details" />
	</template>
	<template #light="props">
		<img src="/img/sweet.png" alt="Go code review showing merged change #657077 'sweet: add typescript-go to go-build benchmark' with approval status and review details" />
	</template>
</LightOrDark>

<!--
Two days later, our repo becomes a Go compiler benchmark.

That's pretty sweet, pun intended.
 -->

---
layout: none
---

<LightOrDark>
	<template #dark="props">
		<img src="/img/thepudds1-dark.png" alt="Go code review #657295 by thepudds showing merged optimization 'avoid reading ir.Node during inner loop of walkOne' that improved TypeScript checker compilation by 30%" />
	</template>
	<template #light="props">
		<img src="/img/thepudds1.png" alt="Go code review #657295 by thepudds showing merged optimization 'avoid reading ir.Node during inner loop of walkOne' that improved TypeScript checker compilation by 30%" />
	</template>
</LightOrDark>

<!--
Later, there's a pair of CLs which speed up the compilation of our checker
package by 5x, which made it into Go 1.25 much to our relief.
-->

---
layout: none
---

<LightOrDark>
	<template #dark="props">
		<img src="/img/thepudds2-dark.png" alt="Go code review #657179 by thepudds showing merged optimization 'improve order of work to speed up analyzing many locations' that gave roughly 5x improvement for TypeScript checker package compilation" />
	</template>
	<template #light="props">
		<img src="/img/thepudds2.png" alt="Go code review #657179 by thepudds showing merged optimization 'improve order of work to speed up analyzing many locations' that gave roughly 5x improvement for TypeScript checker package compilation" />
	</template>
</LightOrDark>

<!--
Later, there's pair of CLs which speed which speeds up the compilation of our checker
package by 5x, which made it into Go 1.25 much to our relief.
-->

---

<img src="/img/filippo2.png" alt="Tweet from Filippo Valsorda showing Go community reaction: TypeScript team rewrites compiler in Go, Go community complains about compilation time being slow, two days later achieves 5x speedup, followed by 'HN: why pick Go anyway?'" />

<style>
  img {
    height: 100%;
    margin: 0 auto;
  }
</style>

<!--
Like Filippo said; with all that support, why pick Go anyway?
-->

---
layout: section
---

# The details

<!--
But, enough about the reaction, let's talk about the details,
the reason you're all here.
-->

---
layout: section
---

# Testing

<!--
One of the main reasons we were so successful in porting the codebase
was due to our extensive testing.
 -->

---

# Testing

```console
$ node ./built/local/run.js
Discovered 326 unittest suites.
Discovering runner-based tests...
Discovered 19583 test files in 33ms.
Starting to run tests using 23 threads...
Batching initial test lists...

  [▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬] ✔ 98894 passing (2m)

  98894 passing (2m)

Finished do-runtests-parallel in 1m 54.4s
```

<!--
TypeScript is nearing 100 thousand tests.
I'm lucky; my machine can run all of the tests in about two minutes.

In CI it's more like 15.
-->

---

# Compiler tests

<!-- dprint-ignore-start -->
```ts [gophercon.ts]
// @strict: true
// @target: es5

const arr = [];
arr.push("hi");
arr.push(1234);

const value: string | number = arr[1];
```
<!-- dprint-ignore-end -->

<!--
A significant number of our tests are in the form of "compiler tests"
where we write some code out and the test harness then runs the compiler on that code, capturing "baselines".
-->

---

# Type baselines

<!-- dprint-ignore-start -->
```ts [gophercon.types] {*|2-3,6-10,13-17}
const arr = [];
>arr : never[]
>[] : never[]

arr.push("hi");
>arr.push("hi") : number
>arr.push : (...items: never[]) => number
>arr : never[]
>push : (...items: never[]) => number
>"hi" : "hi"

arr.push(1234);
>arr.push(1234) : number
>arr.push : (...items: never[]) => number
>arr : never[]
>push : (...items: never[]) => number
>1234 : 1234
```
<!-- dprint-ignore-end -->

<!--
For example, we create type baselines where we walk every node in the AST,
and ask "what's the type at this node", CLICK "what's the type at this node", and so on,
storing the result. If we are working on a change to the compiler and break something,
we'll know because one the baselines will change. These files are committed to the repo,
so we can review them in PRs.

I've also seen these called "golden files" or "snapshots".
-->

---

# Error baselines

<!-- dprint-ignore-start -->
```plaintext [gophercon.errors.txt]
gophercon.ts(2,10): error TS2345: Argument of type '"hi"' is not assignable to parameter of type 'never'.
gophercon.ts(3,10): error TS2345: Argument of type '1234' is not assignable to parameter of type 'never'.


==== gophercon.ts (2 errors) ====
    const arr = [];
    arr.push("hi");
             ~~~~
!!! error TS2345: Argument of type '"hi"' is not assignable to parameter of type 'never'.
    arr.push(1234);
             ~~~~
!!! error TS2345: Argument of type '1234' is not assignable to parameter of type 'never'.
    
    const value: string | number = arr[1];
```
<!-- dprint-ignore-end -->

<!-- We do the same thing for error messages. -->

---

# Emit baselines

<!-- dprint-ignore-start -->
```ts [gophercon.js] {*|6,13}
//// [gophercon.ts]
const arr = [];
arr.push("hi");
arr.push(1234);

const value: string | number = arr[1];


//// [gophercon.js]
const arr = [];
arr.push("hi");
arr.push(1234);
const value = arr[1];
```
<!-- dprint-ignore-end -->

<!--
And for writing out TS and JS files.

You can see here that the difference between TS and JS
is the type annotation.
 -->

---

# Baseline diffing!

<!-- dprint-ignore-start -->
```diff [gophercon.error.txt.diff]
--- old.gophercon.errors.txt
+++ new.gophercon.errors.txt
-<no content>
+gophercon.ts(2,10): error TS2345: Argument of type '"hi"' is not assignable to parameter of type 'never'.
+gophercon.ts(3,10): error TS2345: Argument of type '1234' is not assignable to parameter of type 'never'.
+
+
+==== gophercon.ts (2 errors) ====
+    const arr = [];
+    arr.push("hi");
+             ~~~~
+!!! error TS2345: Argument of type '"hi"' is not assignable to parameter of type 'never'.
+    arr.push(1234);
+             ~~~~
+!!! error TS2345: Argument of type '1234' is not assignable to parameter of type 'never'.
+    
+    const value: string | number = arr[1];
```
<!-- dprint-ignore-end -->

<!--
The key part of this is that we can reimplement that same test harness in Go.
We run the same test against the new compiler, then diff their baselines.
We can even commit those diffs to the new repo as more baselines, and slowly
burn them down as we fix differences between the two compilers.

This was the main way we could track progress and figure out what to focus on.

Sometimes, we'd send a PR and it would fix a couple of baselines. Other times,
we'd fix something and fix half a million lines of baselines!
-->

---

# Testing

## 

```console
$ gotestsum --format-hide-empty-pkg --hide-summary skipped -- ./...
✓  internal/ast (41ms)
✓  internal/compiler (58ms)
✓  internal/execute (137ms)
✓  internal/printer (215ms)
✓  internal/module (402ms)
# ...
✓  internal/checker (2.029s)
✓  internal/parser (1.086s)
✓  internal/project (1.99s)
✓  internal/ls (2.606s)
✓  internal/fourslash/tests/gen (5.584s)
✓  internal/testrunner (11.514s)

DONE 125288 tests, 1113 skipped in 17.710s
```

<!--
And, in the new codebase, tests run a whole lot faster. My machine can run
the whole suite in under 20 seconds.
-->

---
layout: section
---

# Data layout

<!--
In the process of the port, we had to think about data layout, as Go and JavaScript are of course very different in
how the represent objects and memory.
-->

---
src: ./pages/ast.md
---

---

# Allocating nodes

## 

<!-- dprint-ignore-start -->
````md magic-move {lines: false}
```go {*|*}
type Factory struct {/* ... */}

func (f *Factory) NewIdentifier(text string) *Identifier {
    node := &Identifier{}
    node.text = text
    return f.newNode(KindIdentifier, node)
}
```

```go {*|1,4,13,15|1,4,13,15|1,4,13,15|1,4,13,15}
type Factory struct { identifierPool Pool[Identifier] }

func (f *Factory) NewIdentifier(text string) *Identifier {
    node := f.identifierPool.New()
    node.text = text
    return f.newNode(KindIdentifier, node)
}

type Pool struct { space []T }

func (p *Pool[T]) New() (ptr *T) { // The real code is slightly more complex 🙂
    if len(p.space) == 0 {
        p.space = make([]T, 256)
    }
    ptr, p.space = &p.space[0], p.space[1:]
    return ptr
}
```
````
<!-- dprint-ignore-end -->

<img v-click="[1, 2]" src="/img/ast-allocs.png" alt="pprof top allocators, showing NewIdentifier with 36% allocs, etc" />

<!-- Memory allocation animation diagram -->
<div v-click="3" class="memory-diagram">
  <!-- Memory blocks -->
  <div class="memory-block" :class="{ allocated: $clicks >= 4 }">T</div>
  <div class="memory-block" :class="{ allocated: $clicks >= 5 }">T</div>
  <div class="memory-block" :class="{ allocated: $clicks >= 6 }">T</div>
  <div class="memory-block">T</div>
  <div class="memory-block">T</div>
  <div class="memory-block">...</div>

<!-- Allocation arrow -->
<div
    v-motion
    :initial="{ x: 0, opacity: 0 }"
    :click-3="{ opacity: 1 }"
    :click-4="{ x: 54 }"
    :click-5="{ x: 108 }"
    :click-6="{ x: 162 }"
    class="allocation-arrow"
  >
    ↑
  </div>
</div>

<!-- Hack: make clicks extend to the right count. -->

<span v-click="6"></span>

<style>
img {
    margin-top: 20px;
    mask: linear-gradient(to bottom, black 50%, transparent 65%);
    -webkit-mask: linear-gradient(to bottom, black 50%, transparent 65%);
}

.memory-diagram {
    position: absolute;
    top: 40%;
    right: 10%;
    transform: translateY(-50%);
    display: flex;
    align-items: center;
    gap: 4px;
    z-index: 10;
}

.memory-block {
    width: 50px;
    height: 50px;
    border: 2px solid #4a90e2;
    background-color: #e8f4f8;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 18px;
    color: #2c3e50;
    transition: all 0.8s ease;
    position: relative;
}

.memory-block.allocated {
    background-color: #6c757d;
    color: white;
    border-color: #495057;
}

.allocation-arrow {
    font-size: 24px;
    font-weight: bold;
    color: #e74c3c;
    position: absolute;
    bottom: -30px;
    left: -5px;
    transform: translateX(-50%);
    z-index: 11;
}
</style>

<!--
To allocate AST nodes, we have methods on a Factory struct.
The factory is there mainly for bookkeeping reasons I've hidden in the slide, but
the methods are straightforward; they allocate a node, set it up,
then return it.

When we profiled our parser, we found that we had a huge number of allocations.
Some 37% of all allocations during parsing were just identifiers.

In Go, it's not free to allocate memory; you do have to call into the runtime to make
an allocation, so often times reducing the number of allocations can help improve performance.

What we did was to add a "Pool" or "arena", whose job it is to allocate nodes.
It allocates a large slice, then hands out pointers to each element,
until the slice is empty, and repeats.

Now, one downside of this approach is that if any of the items is still
referenced, the entire slice will not be garbage collected. For us, this is fine,
because we either have an entire AST or we don't, but it may not work in all applications.
-->

---

```{*|4,16}
                                                     │ unpooled.txt │              pooled.txt              |
                                                     │    sec/op    │    sec/op     vs base                |
Parse/empty.ts-24                                      189.0n ±  4%    221.3n ± 1%  +17.09% (p=0.000 n=10)
Parse/checker.ts-24                                    41.56m ± 10%    33.53m ± 9%  -19.34% (p=0.000 n=10)
Parse/dom.generated.d.ts-24                            19.44m ±  6%    17.42m ± 8%  -10.37% (p=0.001 n=10)
Parse/Herebyfile.mjs-24                                547.2µ ±  1%    489.8µ ± 3%  -10.49% (p=0.000 n=10)

                                                     │     B/op     │     B/op      vs base                |
Parse/empty.ts-24                                        800.0 ± 0%     880.0 ± 0%  +10.00% (p=0.000 n=10)
Parse/checker.ts-24                                    27.17Mi ± 0%   25.90Mi ± 0%   -4.68% (p=0.000 n=10)
Parse/dom.generated.d.ts-24                            11.31Mi ± 0%   11.03Mi ± 0%   -2.49% (p=0.000 n=10)
Parse/Herebyfile.mjs-24                                426.7Ki ± 0%   458.0Ki ± 0%   +7.33% (p=0.000 n=10)

                                                   │   allocs/op   │  allocs/op   vs base                  |
Parse/empty.ts-24                                         4.000 ± 0%    4.000 ± 0%        ~ (p=1.000 n=10)
Parse/checker.ts-24                                     342.28k ± 0%   12.03k ± 0%  -96.49% (p=0.000 n=10)
Parse/dom.generated.d.ts-24                            138.243k ± 0%   3.112k ± 0%  -97.75% (p=0.000 n=10)
Parse/Herebyfile.mjs-24                                  5.703k ± 0%   1.613k ± 0%  -71.72% (p=0.000 n=10)
```

<!--
Pooling the top-allocating nodes gives a 20% perf boost parsing our old massive checker file,
with 96% fewer allocations, which is a significant improvement.

You pay a little for empty files, but that's an uncommon case.

And, since we have one Factory per parser, each file parse is able to do most of its allocations
without ever synchronizing with anything else.
-->

---

# Composite map keys

````md magic-move {lines: false}
```ts {*|1,4,5}
const substitutionTypes = new Map<string, SubstitutionType>();

function getOrCreateSubstitutionType(baseType: Type, constraint: Type) {
    const id = getTypeId(baseType) + ">" + getTypeId(constraint);
    const cached = substitutionTypes.get(id);
    if (cached) {
        return cached;
    }
    const result = newSubstitutionType(baseType, constraint);
    substitutionTypes.set(id, result);
    return result;
}
```

```go {*|1-4,7,8}
type SubstitutionTypeKey struct {
    baseId       TypeId
    constraintId TypeId
}

func (c *Checker) getOrCreateSubstitutionType(baseType *Type, constraint *Type) *Type {
    key := SubstitutionTypeKey{baseId: baseType.id, constraintId: constraint.id}
    if cached := c.substitutionTypes[key]; cached != nil {
        return cached
    }
    result := c.newSubstitutionType(baseType, constraint)
    c.substitutionTypes[key] = result
    return result
}
```
````

<!--
You Go people take this one for granted, but JavaScript does not have value
types outside primitive values, so no objects as keys. We had to stringify everything. CLICK

This is not as slow as you think (more on that later), but you can see that we have
to stick special characters in there to avoid collisions.

CLICK ... CLICK

In Go we can just use a struct, which is clearer and less error-prone.



Composite map keys like Go is being worked on for JS,
so that'll be nice in the future, but Go's had this for a while.
-->

---

# String encoding

## 

<div class="memory-layout">
  <div class="encoding-section">
    <div class="encoding-title">UTF-16</div>
    <div class="text-label">"Hello 👋" → 16 bytes</div>
    <div class="memory-bar utf16-bar">
      <div class="hex-byte">48</div>
      <div class="hex-byte">00</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">65</div>
      <div class="hex-byte">00</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">6C</div>
      <div class="hex-byte">00</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">6C</div>
      <div class="hex-byte">00</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">6F</div>
      <div class="hex-byte">00</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">20</div>
      <div class="hex-byte">00</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">3D</div>
      <div class="hex-byte">D8</div>
      <div class="hex-byte">4B</div>
      <div class="hex-byte">DC</div>
    </div>
  </div>

<div class="encoding-section">
    <div class="encoding-title">UTF-8</div>
    <div class="text-label">"Hello 👋" → 10 bytes</div>
    <div class="memory-bar utf8-bar">
      <div class="hex-byte">48</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">65</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">6C</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">6C</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">6F</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">20</div>
      <div class="codepoint-separator">|</div>
      <div class="hex-byte">F0</div>
      <div class="hex-byte">9F</div>
      <div class="hex-byte">91</div>
      <div class="hex-byte">8B</div>
    </div>
  </div>
</div>

<style>
.memory-layout {
  max-width: 800px;
  margin: 40px auto;
  font-family: var(--slidev-code-font-family);
}

.encoding-section {
  margin-bottom: 10px;
}

.encoding-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 8px;
  color: var(--slidev-theme-secondary);
}

.text-label {
  font-size: 16px;
  margin-bottom: 12px;
  opacity: 0.8;
}

.memory-bar {
  display: flex;
  flex-wrap: wrap;
  gap: 2px;
  padding: 12px;
  background: rgba(255, 255, 255, 0.05);
  border: 2px solid rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  margin-bottom: 8px;
}

.utf16-bar {
  border-left: 4px solid #ff9500;
}

.utf8-bar {
  border-left: 4px solid #007acc;
}

.hex-byte {
  background: #a855f7;
  color: white;
  padding: 8px 10px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: bold;
  min-width: 24px;
  text-align: center;
  font-family: var(--slidev-code-font-family);
  box-shadow: 0 1px 3px rgba(0,0,0,0.2);
}

.codepoint-separator {
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--slidev-theme-primary);
  font-size: 18px;
  font-weight: bold;
  padding: 0 6px;
  opacity: 0.8;
}

/* Dark mode adjustments */
.dark .memory-bar {
  background: rgba(255, 255, 255, 0.03);
  border-color: rgba(255, 255, 255, 0.08);
}
</style>

<!--
Another fun difference is string encoding.

When we parse files, we hold onto their original source text.
JS (also C#/Java), store strings as UTF-16.
While JS runtimes can be clever about storing ASCII strings,
in practice the strings were still stored as UTF-16 and we
used UTF-16 positions for everything.

Yet, basically all TS source is UTF-8.

Go strings are of course, UTF-8. In the new codebase,
we save memory on most files, and can read files directly as
bytes right into memory.

Getting this to work right was tricky, as we had to audit every place
we did string slicing or calculated positions, but the result is worth it.
-->

---
layout: section
---

# Concurrency

<!--
Of course, this wouldn't be a Go talk without concurrency.

About half of our speedup is from concurrency. We probably wouldn't
have done the port at all had it not been for shared memory concurrency!
-->

---
src: ./pages/concurrency.md
---

---
layout: none
---

<div class="lsp-diagram">
  <div class="editors-container">
    <div class="editor-box vscode">
      <img src="/img/vscode-alt.svg" alt="VS Code" class="editor-logo">
      <div class="editor-label">VS Code</div>
    </div>
    <div class="editor-box neovim">
      <img src="/img/neovim-mark-flat.svg" alt="Neovim" class="editor-logo">
      <div class="editor-label">Neovim</div>
    </div>
    <div class="placeholder-box">
      <div class="placeholder-text">...</div>
    </div>
  </div>
  <div class="connection-section">
    <div class="editor-to-lsp">
      <div class="bidirectional-line"></div>
      <div class="bidirectional-line"></div>
    </div>
    <div class="lsp-center">
      <div class="lsp-box">
        <div class="lsp-title">LSP</div>
        <div class="lsp-subtitle">Language Server Protocol</div>
      </div>
    </div>
    <div class="lsp-to-servers">
      <div class="server-line"></div>
      <div class="server-line"></div>
      <div class="server-line"></div>
    </div>
  </div>
  <div class="servers-container">
    <div class="server-box typescript">
      <img src="/img/typescript-design-assets/ts-logo-128.png" alt="TypeScript" class="server-logo">
      <div class="server-label">tsc --lsp</div>
    </div>
    <div class="server-box go">
      <img src="/img/Go-Logo_Blue.svg" alt="Go" class="server-logo">
      <div class="server-label">gopls</div>
    </div>
    <div class="server-box rust">
      <img src="/img/rust-logo-512x512.png" alt="Rust" class="server-logo">
      <div class="server-label">rust-analyzer</div>
    </div>
    <div class="placeholder-box">
      <div class="placeholder-text">...</div>
    </div>
  </div>
</div>

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p style="text-align: right; opacity: 0.2; font-size: 0.5rem; margin-right: 1rem">
<a href="https://neovim.io/logos/neovim-logos.zip">Neovim logo</a> by Jason Long / <a href="https://creativecommons.org/licenses/by/3.0/">CC BY 3.0</a>,
<a href="https://github.com/rust-lang/rust-artwork/blob/master/logo/rust-logo-512x512.png">Rust logo</a> by ™/®Rust Foundation / <a href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>,
</p>

<style>
.lsp-diagram {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 2rem;
  gap: 2rem;
  min-width: 900px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.editors-container {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  flex-shrink: 0;
}
.editor-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.3);
  min-width: 120px;
}
.editor-box.vscode {
  background: #0065A9;
}
.editor-box.neovim {
  background: rgb(15, 25, 31);
}
.editor-icon {
  font-size: 2rem;
  margin-bottom: 0.8rem;
}
.editor-logo {
  width: 32px;
  height: 32px;
  object-fit: contain;
  margin-bottom: 0.8rem;
  box-shadow: none;
  border: none;
}
.editor-label {
  color: white;
  font-weight: bold;
  font-size: 1rem;
  font-family: var(--slidev-code-font-family);
}
.placeholder-box {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.25rem 0.5rem;
  border: 2px dashed #cbd5e1;
  border-radius: 12px;
  background: rgba(148, 163, 184, 0.1);
  min-width: 120px;
  min-height: 15px;
}
.placeholder-text {
  color: #94a3b8;
  font-size: 1.5rem;
  font-weight: bold;
  font-family: var(--slidev-code-font-family);
}
.lsp-center {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  flex-shrink: 0;
}
.connection-section {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  flex: 1;
  min-height: 200px;
}
.editor-to-lsp {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  flex: 1;
}
.bidirectional-line {
  height: 3px;
  background: linear-gradient(to right, #3b82f6, #1e40af);
  position: relative;
  width: 100%;
}
.bidirectional-line::before {
  content: '';
  position: absolute;
  left: -8px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 0;
  border-top: 8px solid transparent;
  border-bottom: 8px solid transparent;
  border-right: 12px solid #3b82f6;
}
.bidirectional-line::after {
  content: '';
  position: absolute;
  right: -8px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 0;
  border-top: 8px solid transparent;
  border-bottom: 8px solid transparent;
  border-left: 12px solid #1e40af;
}
.lsp-box {
  background: linear-gradient(135deg, #6366f1, #4f46e5);
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 8px 20px rgba(99, 102, 241, 0.3);
  text-align: center;
  flex-shrink: 0;
}
.lsp-title {
  color: white;
  font-size: 6rem;
  font-weight: bold;
  font-family: var(--slidev-code-font-family);
  margin-bottom: 0.5rem;
}
.lsp-subtitle {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1.2rem;
  font-family: var(--slidev-code-font-family);
}
.lsp-to-servers {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  flex: 1;
}
.server-line {
  height: 3px;
  background: linear-gradient(to right, #4f46e5, #1e40af);
  position: relative;
  width: 100%;
}
.server-line::before {
  content: '';
  position: absolute;
  left: -8px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 0;
  border-top: 8px solid transparent;
  border-bottom: 8px solid transparent;
  border-right: 12px solid #4f46e5;
}
.server-line::after {
  content: '';
  position: absolute;
  right: -8px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 0;
  border-top: 8px solid transparent;
  border-bottom: 8px solid transparent;
  border-left: 12px solid #1e40af;
}
.servers-container {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  flex-shrink: 0;
}
.server-box {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  border-radius: 10px;
  box-shadow: 0 6px 16px rgba(0,0,0,0.1);
  min-width: 160px;
}
.server-box.typescript {
  background: linear-gradient(135deg, #3178c6, #235a97);
}
.server-box.go {
  background: linear-gradient(135deg, #00add8, #007d9c);
}
.server-box.rust {
  background: #aa5b2e;
}
.server-logo {
  width: 32px;
  height: 32px;
  object-fit: contain;
  box-shadow: none;
  border: none;
  background: white;
  border-radius: 6px;
  padding: 4px;
}
.server-label {
  color: white;
  font-size: 1rem;
  font-weight: bold;
  font-family: var(--slidev-code-font-family);
}
</style>

<!--
Another key area we are changing things is in the way we talk to editors.
As I said before, the TypeScript toolchain also includes a language server.

In the new codebase, we are switching to LSP, the language server protocol.

Most people familiar with editors are probably asking "what do you mean?
were't you already using LSP?"

But no, we weren't. TypeScript predates LSP and has its own protocol,
which actually inspired the LSP.

People have been asking us to switch to LSP for a while now, and the port
is a great opportunity to do so.

Our old protocol was synchronous, except for
cancellation. This effectively meant we could only ever do one thing
at a time. This limitation led to client-side workarounds like VS Code spawning multiple
language servers so that a more barebones one could answer requests while
the full one was getting ready or working on something else.

But, the language server protocol is asynchronous, meaning we can do more than
one thing at once. And, we _want_ to be able to do more than one thing at once.
That's going to be faster and more straightforward.

But, now we're introducing concurrency. We directly ported a lot of code for
the language server and ended up with a slew of race conditions. Many caught
by the race detector, but other are logical races where things didn't work right.

Just last week, we rewrote the way our language server works to use an immutable snapshot
model, which solved all of our concurrency woes. This isn't a new idea, it's
used in gopls, rust-analyzer, rosyln, but it's new for us.

Our design with disposable independent type checkers also aided in the implementation
of the language server, since we can now spin up more than one checker at a time
to serve semantic requests, like diagnostics at the same time as completions.
-->

---

# LSP testing

<!-- dprint-ignore-start -->
````md magic-move {lines: false}
```ts
/// <reference path="fourslash.ts" />

////let foo /*1*/
/////*2*/
/////*3*/

verify.completions(
    { marker: "1", exact: undefined },
    {
        marker: ["2", "3"],
        exact: completion.globalsPlus([
            {
                name: "foo",
            },
        ]),
    }
);

```

```go
func TestCompletionAfterNewline(t *testing.T) {
	// ...
	const content = `let foo /*1*/
/*2*/
/*3*/`
	f := fourslash.NewFourslash(t, nil /*capabilities*/, content)
	f.VerifyCompletions(t, "1", nil)
	f.VerifyCompletions(t, []string{"2", "3"}, &fourslash.CompletionsExpectedList{
		IsIncomplete: false,
		ItemDefaults: &fourslash.CompletionsExpectedItemDefaults{
			CommitCharacters: &DefaultCommitCharacters,
			EditRange:        Ignored,
		},
		Items: &fourslash.CompletionsExpectedItems{
			Exact: CompletionGlobalsPlus([]fourslash.CompletionsExpectedItem{
				&lsproto.CompletionItem{Label: "foo"},
			}, false),
		},
	})
}
```
````

<!--
Early on, I mentioned our special compiler tests. We also have a similar concept for
testing editor features too.

We didn't want to just drop all of these tests, so we have a script which converts
the old tests into plain Go tests. It's a little verbose comparatively, but it works.

Each of our LSP tests spawns a full LSP server, then sends it messages just like a real
client.

What's cool is that because ASTs are independent and immutable, doing the full end to end
for thousands of tests is actually pretty fast; in our old code, we rarely did a real
server test due to the perf hit. But now, it's much simpler.
-->

---
layout: section
---

# Go gotchas

<!--
Now, it wouldn't be a Gophercon talk without some Go gotchas.
We encountered a few interesting ones during the port.
-->

---

# Variable shadowing

## 

Can you spot the bug?

````md magic-move {lines: false}
```go {*|3,5,10}
func (c *Checker) getUnresolvedSymbolForEntityName(name *ast.Node) *ast.Symbol {
    // ...
    result := c.unresolvedSymbols[path]
    if result == nil {
        result := c.newSymbol(ast.SymbolFlagsTypeAlias, text)
        c.unresolvedSymbols[path] = result
        result.Parent = parentSymbol
        c.declaredTypeLinks.Get(result).declaredType = c.unresolvedType
    }
    return result
}
```

```go
func (c *Checker) getUnresolvedSymbolForEntityName(name *ast.Node) *ast.Symbol {
    // ...
    result := c.unresolvedSymbols[path]
    if result == nil {
        result = c.newSymbol(ast.SymbolFlagsTypeAlias, text)
        c.unresolvedSymbols[path] = result
        result.Parent = parentSymbol
        c.declaredTypeLinks.Get(result).declaredType = c.unresolvedType
    }
    return result
}
```
````

<v-click>

More on the `go/analysis` analyzer:
[jakebailey.dev/posts/go-shadowing](https://jakebailey.dev/posts/go-shadowing/)

</v-click>

<!--
Here's a fun question for the audience; can you spot the bug?

There are two declarations named `result` CLICK, but the code intended to return
the second one. The intended code is just one character away. CLICK

This bug happened so often in ported code that I wrote a `go/analysis` analyzer
to catch it. CLICK

The Go team has a similar analyzer called `shadow`, but I found that it had
too many false positives for our codebase. My version uses control flow analysis
to only flag cases where the shadowing has an effect on the code. It'd be cool
to upstream this analyzer at some point.

After enabling that analyzer on the repo, we never had a shadowing bug again.
-->

---

# Method values

## 

````md magic-move {lines: false}
```ts {*|5,8}
function createBinder(sourceFile: SourceFile) {
    // ...

    function bindEachChild(node: Node) {
        forEachChild(node, bind);
    }

    function bind(node: Node) {/*... */}
}
```

```go
type Binder struct {
    // ...
}

func Bind(node *ast.SourceFile) {
    b := &Binder{/* ... */}
    // ...
}

func (b *Binder) bindEachChild(node *ast.Node) {
    node.ForEachChild(b.bind)
}

func (b *Binder) bind(node *ast.Node) {
    // ...
}
```
````

<!--
Now, if you remember, in the old codebase our code looked something like this.
The binder closed over data and functions.

CLICK

In this bit, we're binding all of the children of a node with
a forEachChild helper function.

CLICK

In Go, this is very similar, the only difference is that we are using methods
instead of local functions.
-->

---

# Method values

## 

<br>

<img src="/img/bind-method-allocs.png" alt="Screenshot of pprof for the bindEachChild method, showing many allocs from the method binding" class="bind-pprof" />

<style>
  .bind-pprof {
    width: 100%;
  }
</style>

<!--
But, we profiled the code, and pprof revealed an issue; this code does a lot of allocations! Why?
-->

---

# "Pre-binding" methods

## 

````md magic-move {lines: false}
```go {*|11}
type Binder struct {
    // ...
}

func Bind(node *ast.SourceFile) {
    b := &Binder{/* ... */}
    // ...
}

func (b *Binder) bindEachChild(node *ast.Node) {
    node.ForEachChild(b.bind) // <-- Allocation each time
}

func (b *Binder) bind(node *ast.Node) {
    // ...
}
```

```go {*|3,8,13,16}
type Binder struct {
    // ...
    bind func(node *ast.Node)
}

func Bind(node *ast.SourceFile) {
    b := &Binder{/* ... */}
    b.bind = b.bindWorker // <-- Allocate once
    // ...
}

func (b *Binder) bindEachChild(node *ast.Node) {
    node.ForEachChild(b.bind)
}

func (b *Binder) bindWorker(node *ast.Node) {
    // ...
}
```
````

<!--
Compiler can't prove anything about what ForEachChild does,
so no inlining, param it always escapes. CLICK So the method value
is recreated each time. This operation looks cheap, but is not cheap at all!

The way we fixed this was to "pre-bind" the method CLICK, storing it in a field
when the Binder is created. This way the method value is only allocated once
for each binder.
-->

---

# "Pre-binding" methods

```plaintext {*|3,7,11}
         │   old.txt   │               new.txt               │
         │   sec/op    │   sec/op     vs base                │
Bind-20    24.74m ± 2%   20.55m ± 1%  -16.94% (p=0.000 n=10)

         │   old.txt    │               new.txt                │
         │     B/op     │     B/op      vs base                │
Bind-20    9.776Mi ± 0%   8.420Mi ± 0%  -13.87% (p=0.000 n=10)

         │   old.txt    │               new.txt               │
         │  allocs/op   │  allocs/op   vs base                │
Bind-20    102.56k ± 0%   13.69k ± 0%  -86.65% (p=0.000 n=10)
```

<!--
This one trick speeds up binding by 17 percent, dropping nearly 90
percent of the allocations.
-->

---

# Callbacks

````md magic-move {lines: false}
```ts {*|3-8|15}
function parseSourceFile(fileName: string, text: string): SourceFile {
    // ...
    function lookAhead<T>(callback: () => T): T {
        // ... save state
        const result = callback();
        // ... restore state
        return result;
    }

    function isYieldExpression(): boolean {
        if (token() === SyntaxKind.YieldKeyword) {
            if (inYieldContext()) {
                return true;
            }
            return lookAhead(nextTokenIsIdentifierOrKeywordOrLiteralOnSameLine);
        }
        return false;
    }
}
```

```go {*|13}
func (p *Parser) lookahead(callback func() bool) bool {
    // ... save state
    result := callback()
    // ... restore state
    return result
}

func (p *Parser) isYieldExpression() bool {
    if p.token() == ast.KindYieldKeyword {
        if p.inYieldContext() {
            return true
        }
        return p.lookahead(p.nextTokenIsIdentifierOrKeywordOrLiteralOnSameLine)
    }
    return false
}
```

```go {*|1,3,13}
func (p *Parser) lookahead(callback func(p *Parser) bool) bool {
    // ... save state
    result := callback(p)
    // ... restore state
    return result
}

func (p *Parser) isYieldExpression() bool {
    if p.token() == ast.KindYieldKeyword {
        if p.inYieldContext() {
            return true
        }
        return p.lookahead((*Parser).nextTokenIsIdentifierOrKeywordOrLiteralOnSameLine)
    }
    return false
}
```
````

<!--
Another similar example is in our parser, where we used to have a lookahead
function CLICK.

You'd give it a callback, and it would then speculatively parse, then
rewind the parser state when done, returning the result

CLICK

In some cases, we pass in a local function, which necessarily accesses other information
in the parser.

CLICK

In Go, this turns into a method value, which again could allocate. CLICK

But, since lookahead is a method on the parser, we can instead pass in a method
EXPRESSION instead of a method value, and just explicitly call it with the parser
as the first argument. CLICK
-->

---

# String building

## 

In Go, this is a big no-no. <span v-click.at="+1">Use `strings.Builder`
instead.</span>

````md magic-move {lines: false}
```go
result := ""
for _, s := range strings {
    result += s // Big no-no
}
```

```go
var result strings.Builder
for _, s := range strings {
    result.WriteString(s)
}
```
````

<!--
Here's another one.

In Go, this is a big no-no. Every time the string is concatenated,
a new string is allocated. You're supposed to use `strings.Builder`.
-->

---

# String building

## 

But in JS, this is totally fine.

```ts
let result = "";
for (const s of strings) {
    result += s;
}
```

<v-click>

"Cons string" -- roughly `struct { Left string; Right string }`

<div class="cons-string-diagram">
  <div class="string-node">"foo"</div>
  <div class="arrow">→</div>
  <div class="string-node">","</div>
  <div class="arrow">→</div>
  <div class="string-node">"bar"</div>
  <div class="arrow">→</div>
  <div class="string-node">","</div>
  <div class="arrow">→</div>
  <div class="string-node">"baz"</div>
</div>

```ts
const map = new Map<string, any>();
const x = map.get(result); // Won't flatten the string when hashing/comparing!
```

</v-click>

<style>
.cons-string-diagram {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  margin: 20px 0;
  padding: 20px;
}

.string-node {
  background: #a855f7;
  color: white;
  padding: 8px 16px;
  border-radius: 6px;
  font-family: var(--slidev-code-font-family);
  font-size: 14px;
  font-weight: bold;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  min-width: 40px;
  text-align: center;
}

.arrow {
  font-size: 20px;
  font-weight: bold;
  color: var(--slidev-theme-primary);
  opacity: 0.8;
}

/* Dark mode adjustments */
.dark .string-node {
  box-shadow: 0 2px 8px rgba(255, 255, 255, 0.1);
}
</style>

<!--
But in JavaScript, this is totally fine.
The runtimes optimize this.

CLICK

In V8, it's represented as a "cons string", which is functional programming
jargon that just means, a tree of strings.
In this case, we're always appending so it looks like a chain.

Strings joined with `+`, .join, etc, are not flattened until
they are observed. Hashing doesn't have to flatten either, it just walks all of the strings.

Those stringified map keys I showed earlier are efficient because
querying the caches don't actually produce the whole string, it just
hashes the cons string.

The fact that we had these in TS though led to perf bugs in Go.

Thankfully, pprof will point this one out.

It'd be really cool to have these in Go, though I'm not sure exactly how that would work.
-->

---

# What we miss

<v-clicks depth="2">

- Compile-time `nil` safety
- `nil` coalescing (`?.`, `??`)
- Union types, narrowing
- Generic methods
- Ternary operator
- ...

But, we're willing to go through some pain if it means TypeScript is faster for
our users.

</v-clicks>

<!--
And of course, the biggest friction of all were the language
features we lost when leaving TypeScript.

That's nil safety, nil coalescing, union types, narrowing, generic methods,
ternary operator.

But, we're willing to go through some pain if it means TypeScript is faster for
our users.
 -->

---
layout: section
---

# Where are we today?

---
layout: two-cols
---

# Preview builds

## 

<br>

```sh
npm install -D @typescript/native-preview
npx tsgo
```

"TypeScript (Native Preview)" in VS Code:
[jakebailey.dev/go/ts-native-preview-ext](https://jakebailey.dev/go/ts-native-preview-ext)

<br>

![NPM package statistics showing TypeScript Native Preview with 192,788 weekly downloads, version 7.0.0-dev.20250819.1, and Apache-2.0 license, demonstrating significant adoption of the Go-based TypeScript compiler](/img/native-preview-package.png)

::right::

<img src="/img/slack1.png" alt="Slack screenshot showing TypeScript Native Preview usage" class="slack" />

<br>

> **John Firebaugh (Figma)**: Experience report for tsgo at Figma: it's
> typechecking our frontend monolith (2.8mloc) successfully, with a ~5x speed
> improvement (3m07s -> 37s). Considering the size of the codebase, it was
> remarkably easy to get working.

<style>
  /* .slack {
    display: block;
    margin: auto;
    position: relative;
    top: 50%;
    transform: translateY(-50%);
  } */
</style>

<!--
We put out a preview build a few months ago.
It's even more feature complete.
Editor support has been constantly improving.
Build mode for multi-projects was just merged last week.

Our preview package is getting nearly 200 thousand weekly downloads; I'm not sure
who all of these people are but it's exciting to see.

Some big TS users have already switched over.
Slack switched over. Their build used to be nearly 6 minutes,
but is now roughly 40 seconds, about 9 times faster.

Figma just get it working last week and seeing roughly 5x faster.

VS Code is starting to use it to build themselves.
-->

---

# `tsgolint`

## 

30x faster typed linting!
[github.com/oxc-project/tsgolint](https://github.com/oxc-project/tsgolint)

![Performance comparison table showing tsgolint vs ESLint + typescript-eslint on AMD Ryzen 7 5800H (8 cores, 16 threads). Results show dramatic speedups: microsoft/vscode from 167.8s to 4.89s (34x faster), microsoft/typescript from 47.4s to 2.10s (23x faster), typeorm/typeorm from 27.3s to 0.93s (29x faster), and vuejs/core from 20.7s to 0.95s (22x faster)](/img/tsgolint-results.png)

<style>
  img {
    width: 75%;
    margin: 0 auto;
  }
</style>

<!--
There's also a linter being worked on that uses our code to implement typed lint rules
that previously required the TypeScript compiler API.
This new linter ported the rules into Go and got something like a 30x speedup,
and that's apples to apples too, same config and everything.
-->

---

![Code screenshot showing Go functions using //go:linkname directives to access internal TypeScript Go compiler APIs, demonstrating how tsgolint hooks into the TypeScript checker internals](/img/tsgolint-hack.png)

<span class="shocked-emoji">😱</span>

<style>
  img {
    width: 95%;
    margin: 0 auto;
  }

  .shocked-emoji {
    position: absolute;
    top: 50%;
    left: 25%;
    transform: translateY(-50%) scale(0.2) rotate(-15deg);
    font-size: 40em;
    z-index: 10;
  }
</style>

<!--
Of course, it only took the most cursed hacks to do it.

It's funny, even when we switch languages, the TS ecosystem finds a way into our internals!
-->

---
layout: section
---

# What's next?

<!--
We're really far along in the port, but there's still a lot of work to do.

We're currently working on bunch of great stuff.

- Much of our effort is currently being spent on editor functionality
- Many editor features are nearly reimplemented
  - Including rename and auto imports
  - And the rest of the LSP
- Our big language server refactor means a more straightforward path to implementing
  speculative edits, refactors, and MCP.
- We're finishing up emit transforms
- In the future, we'll be improving file watching, and contributing to the LSP to add all of the special
  features we (and likely other languages like Go) need.
- For me personally, I'm excited to get Wasm going and figure out how we can get Wasm running faster.
- I'd also like to get a Go API out there, though it's going to be a challenge to meet the high
  bar of the Go1 promise.
- And of course, we're always working on performance improvements
  - we are getting a load of feedback from the community on their large and complicated codebases.
- We're still iterating on the main TypeScript codebase, and TypeScript 6.0 will include
  a bunch of deprecations and changes to help smooth over the transition to TypeScript 7.0,
  the release that will be powered by Go.

-->

---
layout: section
---

# The future is bright!

<div class="ts-loves-go">
  <img src="/img/typescript-design-assets/ts-logo-512.svg" alt="TypeScript logo" class="ts-logo" />
  <span class="heart">♥</span>
  <img src="/img/Go-Logo_Blue.svg" alt="Go logo" class="go-logo" />
</div>

<style>
  .ts-loves-go {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 40px;
    margin: 30px auto;
  }

  img {
    box-shadow: none !important;
    border-radius: 0 !important;
  }

  .ts-logo {
    height: 100px;
    width: 175px;
    object-fit: contain;
  }

  .go-logo {
    height: 150px;
    width: 175px;
    object-fit: cover;
    object-position: right center;
  }

  .heart {
    font-size: 4rem;
    color: #e74c3c;
    display: flex;
    align-items: center;
    justify-content: center;
    line-height: 1;
  }
</style>

<!--
So, in summary, the future is bright!
We're really excited to continue this effort, and Go's a huge part of that.
I really think Go has been a great fit for the port.

It's also been great to talk with the Go team and cross-pollinate ideas.
We had so many great conversations, especially this week at GopherCon.

I'm really excited for the future.
-->

---

# Thank you!

## 

Find me online!

- [jakebailey.dev](https://jakebailey.dev)
- [@jakebailey.dev](https://bsky.app/profile/jakebailey.dev) on Bluesky
- [@jakebailey](https://github.com/jakebailey) on GitHub

Try out the preview and give us feedback!

- `npm install -D @typescript/native-preview; npx tsgo`
- "TypeScript (Native Preview)" in VS Code:
  [jakebailey.dev/go/ts-native-preview-ext](https://jakebailey.dev/go/ts-native-preview-ext)

Find the code at:
[github.com/microsoft/typescript-go](https://github.com/microsoft/typescript-go)

<div class="talk-info">
<QRCode id="talk-qrcode" :width="175" :height="175" type="svg" :dotsOptions="{ color: 'var(--slidev-code-foreground)' }" :backgroundOptions="{ color: 'transparent' }"
data="https://jakebailey.dev/talk-gophercon-2025" image="/img/typescript-design-assets/ts-logo-512.svg" :imageOptions="{ margin: 2 }" />

[jakebailey.dev/talk-gophercon-2025](https://jakebailey.dev/talk-gophercon-2025)

</div>

<img src="/img/me.jpg" alt="Professional headshot of Jake Bailey, a man with brown hair and beard wearing an olive green t-shirt, photographed outdoors by a body of water at sunset" id="profile-pic" />

<style>
  .talk-info {
    position: relative;
    text-align: right;
    padding-top: 0;
  }
  #talk-qrcode {
    position: absolute;
    top: -200px;
    right: 0;
  }
  .talk-info p {
    margin: 0;
    clear: both;
  }
  #profile-pic {
    position: absolute;
    top: 24%;
    left: 35%;
    width: 10%;
    border-radius: 50%;
    object-fit: cover;
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
  }
</style>

<!--
Thank you all for sticking around; please give the preview a try and let us know what you think!

See you out in the hallway!
-->
