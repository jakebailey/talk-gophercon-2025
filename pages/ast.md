# AST layout

## 

<div class="node-interface-diagram">
  <div class="interface-container">
    <div class="interface-title">type Node interface</div>
    <div class="interface-methods">
      <div class="method">Kind() Kind</div>
      <div class="method">Pos() int32</div>
      <div class="method">End() int32</div>
      <div class="method">Parent() Node</div>
    </div>
  </div>
  <div class="implementing-structs">
    <div class="struct-container">
      <div class="struct-title">type FunctionDeclaration struct</div>
      <div class="struct-fields">
        <div class="field">pos,&nbsp;end&nbsp;int32</div>
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">parent&nbsp;&nbsp;&nbsp;Node</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Identifier</div>
        <div class="field" :class="$clicks == 3 ? 'highlight-node' : ''">params&nbsp;&nbsp;&nbsp;[]*Parameter</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">body&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Block</div>
      </div>
    </div>
    <div class="struct-container">
      <div class="struct-title">type CallExpression struct</div>
      <div class="struct-fields">
        <div class="field">pos,&nbsp;end&nbsp;int32</div>
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">parent&nbsp;&nbsp;&nbsp;Node</div>
        <div class="field" :class="($clicks == 1 || $clicks == 2) ? 'highlight-node' : ''">expr&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Node</div>
        <div class="field" :class="$clicks == 3 ? 'highlight-node' : ''">args&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[]Node</div>
      </div>
    </div>
    <div class="struct-container">
      <div class="struct-title">type IfStatement struct</div>
      <div class="struct-fields">
        <div class="field">pos,&nbsp;end&nbsp;&nbsp;&nbsp;int32</div>
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">parent&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Node</div>
        <div class="field" :class="($clicks == 1 || $clicks == 2) ? 'highlight-node' : ''">condition&nbsp;&nbsp;Node</div>
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">then&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Node</div>
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">else&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Node</div>
      </div>
    </div>
    <div class="struct-container">
      <div class="struct-title">type Identifier struct</div>
      <div class="struct-fields">
        <div class="field">pos,&nbsp;end&nbsp;int32</div>
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">parent&nbsp;&nbsp;&nbsp;Node</div>
        <div class="field">text&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;string</div>
      </div>
    </div>
  </div>
</div>

<!-- Hack: make clicks extend to the right count. -->

<span v-click="3"></span>

<style>
.node-interface-diagram {
  position: relative;
  padding: 40px 20px;
  height: 400px;
  width: 100%;
}

.interface-container {
  position: absolute;
  top: 20px;
  left: 20px;
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  border-radius: 12px;
  padding: 16px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.15);
  min-width: 200px;
}

.interface-title {
  color: white;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 12px;
  font-family: var(--slidev-code-font-family);
}

.interface-methods {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.method {
  background: rgba(255,255,255,0.2);
  color: white;
  padding: 6px 10px;
  border-radius: 6px;
  font-size: 12px;
  font-family: var(--slidev-code-font-family);
  text-align: left;
}

.implementing-structs {
  position: absolute;
  top: 20px;
  right: 20px;
  left: 280px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 16px;
  height: 320px;
}

.struct-container {
  background: linear-gradient(135deg, #047857, #064e3b);
  border-radius: 10px;
  padding: 14px;
  box-shadow: 0 6px 16px rgba(0,0,0,0.1);
  min-height: 190px;
}

.struct-title {
  color: white;
  font-size: 13px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;
  font-family: var(--slidev-code-font-family);
}

.struct-fields {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.field {
  background: rgba(255,255,255,0.2);
  color: white;
  padding: 2px 4px;
  border-radius: 4px;
  font-size: 10px;
  font-family: var(--slidev-code-font-family);
  text-align: left;
  word-break: break-word;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.field.highlight-node {
  outline: 3px solid #f59e0b;
  outline-offset: -3px;
}
</style>

<!--
For our AST (abstract syntax tree), the most obvious layout is a Node interface,
with individual node types implementing it.

But, this has downsides.

- Node fields
	- Within the AST, we store a huge number of references CLICK and those often appear as Node interface values.
	- Interfaces are fat pointers, so each reference is two pointers.
	- Compiling VS Code allocates more than 9 million nodes
		- VS Code is 1.5 million lines of code, we know of some repos with 15 million!
	- Maybe this isn't that much, but what's worse is that most of
		them are nil, only there just in case. For example, most
		if statements don't have an "else" clause. All of those unused fields are just sitting there
		in the tree, taking up space.
	- Worst of all, we kept assigning nil pointers into Node interface values
		- Classic Go mistake, but TS doesn't have this problem thanks to union types, so when porting code, we hit it often.
- CLICK Further, we had this odd dissonance between some specific type fields and Node fields
	- Sometimes you'd have a Node, sometimes a specific type, so to make helpers work you'd
	  often need be forced to use Node anyway. And sometimes, our AST has to change, and you might
	  have a child that was previously only one type, but now it could be two, so that would just
	  turn into Node again, and that cascades out into refactors in the rest of the codebase.
- CLICK Node slices
	- You'll also note that the two slices for child nodes are different between these two
	  structs. These are the most specific types we can have, which is good for safety,
	  but the effect is that it's really hard to write code that works with multiple
	  different slice types with different nodes. Not even generics can help in some cases,
	  and we ended up needing to do copies. If you search "array covariance" you'll find
	  what I mean.
-->

---

# Node pointers everywhere

<div class="node-interface-diagram">
  <div class="interface-container" :class="$clicks == 1 ? 'highlight-container' : ''">
    <div class="interface-title">type Node struct</div>
    <div class="interface-methods">
      <div class="method">kind&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kind</div>
      <div class="method">pos,&nbsp;end&nbsp;int32</div>
      <div class="method">parent&nbsp;&nbsp;&nbsp;*Node</div>
      <div data-id="node-self" class="method" :class="$clicks == 3 || $clicks == 4 ? 'highlight-node' : ''">self&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nodeSelf</div>
    </div>
  </div>
  <div class="implementing-structs">
    <div class="struct-container" data-id="function-declaration">
      <div class="struct-title">type FunctionDeclaration struct</div>
      <div class="struct-fields">
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">Node</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">name&nbsp;&nbsp;&nbsp;*Node</div>
        <div class="field" :class="$clicks == 5 ? 'highlight-node' : ''">params&nbsp;[]*Node</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">body&nbsp;&nbsp;&nbsp;*Node</div>
      </div>
    </div>
    <div class="struct-container" data-id="call-expression">
      <div class="struct-title">type CallExpression struct</div>
      <div class="struct-fields">
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">Node</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">expr&nbsp;*Node</div>
        <div class="field" :class="$clicks == 5 ? 'highlight-node' : ''">args&nbsp;[]*Node</div>
      </div>
    </div>
    <div class="struct-container" data-id="if-statement">
      <div class="struct-title">type IfStatement struct</div>
      <div class="struct-fields">
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">Node</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">condition&nbsp;*Node</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">then&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Node</div>
        <div class="field" :class="$clicks == 2 ? 'highlight-node' : ''">else&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Node</div>
      </div>
    </div>
    <div class="struct-container" data-id="identifier">
      <div class="struct-title">type Identifier struct</div>
      <div class="struct-fields">
        <div class="field" :class="$clicks == 1 ? 'highlight-node' : ''">Node</div>
        <div class="field">text&nbsp;string</div>
      </div>
    </div>
  </div>
</div>

<FancyArrow seed="1" roughness="0" width="3" v-click="[4]" from="[data-id=node-self]@(90%,50%)" to="[data-id=function-declaration]@top" color="orange" arc="0.5" animated animation-duration="500" />
<FancyArrow seed="1" roughness="0" width="3" v-click="[4]" from="[data-id=node-self]@(90%,50%)" to="[data-id=call-expression]@top" color="orange" arc="0.5" animated animation-duration="500" />
<FancyArrow seed="1" roughness="0" width="3" v-click="[4]" from="[data-id=node-self]@(90%,50%)" to="[data-id=if-statement]@top" color="orange" arc="0.1" animated animation-duration="500" />
<FancyArrow seed="1" roughness="0" width="3" v-click="[4]" from="[data-id=node-self]@(90%,50%)" to="[data-id=identifier]@top" color="orange" arc="0.1" animated animation-duration="500" />

<div class="disclaimer"><em>*simplified for these slides</em> 🙂</div>

<!-- Hack: make clicks extend to the right count. -->

<span v-click="5"></span>

<style>
.node-interface-diagram {
  position: relative;
  padding: 40px 20px;
  height: 400px;
  width: 100%;
}

.interface-container {
  position: absolute;
  top: 20px;
  left: 20px;
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  border-radius: 12px;
  padding: 16px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.15);
  min-width: 200px;
}

.interface-title {
  color: white;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 12px;
  font-family: var(--slidev-code-font-family);
}

.interface-methods {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.method {
  background: rgba(255,255,255,0.2);
  color: white;
  padding: 6px 10px;
  border-radius: 6px;
  font-size: 12px;
  font-family: var(--slidev-code-font-family);
  text-align: left;
}

.implementing-structs {
  position: absolute;
  top: 20px;
  right: 20px;
  left: 280px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 16px;
  height: 320px;
}

.struct-container {
  background: linear-gradient(135deg, #047857, #064e3b);
  border-radius: 10px;
  padding: 14px;
  box-shadow: 0 6px 16px rgba(0,0,0,0.1);
  min-height: 190px;
}

.struct-title {
  color: white;
  font-size: 13px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;
  font-family: var(--slidev-code-font-family);
}

.struct-fields {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.field {
  background: rgba(255,255,255,0.2);
  color: white;
  padding: 2px 4px;
  border-radius: 4px;
  font-size: 10px;
  font-family: var(--slidev-code-font-family);
  text-align: left;
  word-break: break-word;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.field.highlight-node {
  outline: 3px solid #f59e0b;
  outline-offset: -3px;
}

.method {
  background: rgba(255,255,255,0.2);
  color: white;
  padding: 6px 10px;
  border-radius: 6px;
  font-size: 12px;
  font-family: var(--slidev-code-font-family);
  text-align: left;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.method.highlight-node {
  outline: 3px solid #f59e0b;
  outline-offset: -3px;
}

.disclaimer {
  position: absolute;
  bottom: 160px;
  left: 60px;
  opacity: 0.7;
  color: var(--slidev-theme-secondary);
}

.interface-container {
  transition: all 0.3s ease;
}

.interface-container.highlight-container {
  box-shadow: 0 8px 20px rgba(0,0,0,0.15);
  outline: 4px solid #f59e0b;
  outline-offset: -4px;
}
</style>

<!--
Early on, we switched to a new AST representation, in which
everything is a struct.

CLICK

The base Node struct contains
the common fields that we always need to access, including
the node kind, its position in the source text, and its parent.
That base Node is then embedded in each of the specific AST node types.

CLICK

We then only ever pass around Node pointers, not specific types.
We lose safety in many cases, but a lot of the time we are just
passing things around and are just looking at the common fields.
This also means that we don't box any nils in interfaces, as we
only ever have concrete Node pointers, and so that whole slew of
porting bugs disappeared

But, if you have a Node pointer, you still need to get back to the more
specific type. And so, Node contains a "self pointer" CLICK that via an interface
points back to the original node. CLICK

Node slices now just contain Node pointers, so we can write
code that works on any of them.

 -->

---

```go
func (n *Node) AsIdentifier() *Identifier               { return n.self.(*Identifier) }
func (n *Node) AsPrivateIdentifier() *PrivateIdentifier { return n.self.(*PrivateIdentifier) }
func (n *Node) AsQualifiedName() *QualifiedName         { return n.self.(*QualifiedName) }

func (n *Node) Text() string {
	switch n.Kind {
	case KindIdentifier:
		return n.AsIdentifier().Text
	case KindPrivateIdentifier:
		return n.AsPrivateIdentifier().Text
	// ...
	case KindJsxNamespacedName:
		return n.AsJsxNamespacedName().Namespace.Text() + ":" + n.AsJsxNamespacedName().name.Text()
	case KindJSDocText:
		return strings.Join(n.AsJSDocText().text, "")
	// ...
	}
	panic(fmt.Sprintf("Unhandled case in Node.Text: %T", n.self))
}
```

<!--
Finally, since Node is no longer an interface, it can have methods. We define
helpers for downcasts, but also helpers to access common fields and computations.

Now to be clear, this layout is not perfect. As I said, there is a loss
in safety. It may be clearer for the average Go project to just use interfaces.
But for us, this was a better layout for the port.
-->
