>#Section 2：React组件
>&nbsp;&nbsp;&nbsp;&nbsp;组件让您将 UI 拆分成独立的、 可重用的块，从而实现高度模块化。从概念上讲，组件与 JavaScript 函数一样。可以接受任意输入，并返回React元素来渲染显示内容。

>##Functional和组件类
>定义React组件最简单的方式是写一个Javascript方法。
>
>     function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }
>&nbsp;&nbsp;&nbsp;&nbsp;React组件接受一个简单的“props”对象变量并返回React元素，我们称这样的组件为“functional”，因为它看起来想javascript方法。
>我们也可以通过ES6类的方式来定义组件。
>
>     class Welcome extends React.Component {
        render() {
            return <h1>Hello, {this.props.name}</h1>;
        }
     }
>&nbsp;&nbsp;&nbsp;&nbsp;上面两个组件是等价的，不过类还有一些其他的属性，我们这里暂时不讨论了，根据代码简洁原则，我们这里使用functional组件。
>##使用组件
>之前，我们仅用React元素表示 DOM 标签︰
>
>     const element = <div />;
   
>然而，React元素还可以用来表示用户定义的组件︰

>     const element = <Welcome name="Sara" />;
    ReactDOM.render(
        element,
        document.getElementById('root')
    );
>&nbsp;&nbsp;&nbsp;&nbsp;当React识别到这个元素是自定义的组件，它将JSX属性作为一个简单对象(props)传递到自定义组件中，比如上面的Welcome组件中的属性name,通过props.name传递到组件中。

>     function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }
>我们来分析下解析过程：
>
1. 首先，`ReactDOM.render()`方法在root节点加载`<Welcome name="Sara" />`元素。
2. `Welcome`元素不是html标签，React识别到它是一个组件，React调用Welcome组件并使用`{name: 'Sara'}`作为props参数。
3. `Welcome`组件返回`<h1>Hello, Sara</h1>`元素。
4. 最后在`root`节点加载`<h1>Hello, Sara</h1>`。
>********
><span style="color:red">注：React组件总是以一个大写英文单词开始。
>比如`<div />`是一个DOM标签，但是`<Welcome/>`作为组件是以一个大写单词开始的。</span>
>##组件构成
>组件可以引用其他的组件，比如我们可以创建一个App组件，让它引用Welcome组件。

>     function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }
>
    function App() {
        return (
            <div>
            <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
    );
    }
>
    ReactDOM.render(
      <App />,
      document.getElementById('root')
    );
>通常情况下，新React App最顶端有一个唯一App组件。但是，如果你是在现有的项目中使用React，你可以按照自己的方式由下而上的加入组件。
>***
><span style="color:red">注：组件必须返回一个唯一的根节点，就像上面必须将所有的`<Welcome/>`组件包含在`<div/>`,而不是返回多个同级`<Welcome/>`节点。<span>
>##拆分组件
>&nbsp;&nbsp;&nbsp;&nbsp;不要怕拆分组件，看看下面的例子，思考下`Comment`组件。
>
>     function Comment(props) {
	  return (
	    <div className="Comment">
	      <div className="UserInfo">
	        <img className="Avatar"
	          src={props.author.avatarUrl}
	          alt={props.author.name}
	        />
	        <div className="UserInfo-name">
	          {props.author.name}
	        </div>
	      </div>
	      <div className="Comment-text">
	        {props.text}
	      </div>
	      <div className="Comment-date">
	        {formatDate(props.date)}
	      </div>
	    </div>
	  );
	}
>它接受`author`(object)，`text`(string)和`date`(date)作为`props`属性，输出评论信息。
>此组件如果要修改的话可能比较麻烦，因为里面有很多嵌套，也很难被重用。如果我们把它提取出几个小的组件看起来就会好很多。

>首先，把Avatar提取出来：
>
    function Avatar(props) {
	  return (
	    <img className="Avatar"
	      src={props.user.avatarUrl}
	      alt={props.user.name}
	    />
	  );
	}
>然后优化`Comment`组件：
>
	function Comment(props) {
	  return (
	    <div className="Comment">
	      <div className="UserInfo">
	        <Avatar user={props.author} />
	        <div className="UserInfo-name">
	          {props.author.name}
	        </div>
	      </div>
	      <div className="Comment-text">
	        {props.text}
	      </div>
	      <div className="Comment-date">
	        {formatDate(props.date)}
	      </div>
	    </div>
	  );
	}
>下一步我们继续提取`UserInfo`组件：
>
	function UserInfo(props) {
	  return (
	    <div className="UserInfo">
	      <Avatar user={props.user} />
	      <div className="UserInfo-name">
	        {props.user.name}
	      </div>
	    </div>
	  );
	}
优化后：
>
	function Comment(props) {
	  return (
	    <div className="Comment">
	      <UserInfo user={props.author} />
	      <div className="Comment-text">
	        {props.text}
	      </div>
	      <div className="Comment-date">
	        {formatDate(props.date)}
	      </div>
	    </div>
	  );
	}
>最开始可能会觉得提取组件是一个单调的体力劳动，但是在大型项目中使用可重用的组件是非常有好处的。一个好的规则是如果你的某一部分UI被多次使用，或者是比较复杂的组件，你应该做成可重用的组件。