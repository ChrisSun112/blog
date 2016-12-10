>#Section 3. React state
>看一下React实现时钟的例子：
>
    import React from 'react';
    import ReactDOM from 'react-dom';
    function tick() {
	  const element = (
	    <div>
	      <h1>Hello, world!</h1>
	      <h2>It is {new Date().toLocaleTimeString()}.</h2>
	    </div>
	  );
	  ReactDOM.render(
	    element,
	    document.getElementById('root')
	  );
	}
>	
	setInterval(tick, 1000);
>然而，上面是通过`setInterval`方法每间隔1s调用tick方法更新UI。理想的情况是我们想通过下面的方式，让`Clock`自动更新。
>
	ReactDOM.render(
	  <Clock />,
	  document.getElementById('root')
	);
>为了实现这个功能，我们向`Clock`组件中增加"state"。State与props相识，但是它是组件私有的，由组件控制。我们前面提到过，类定义的组件有一些额外的功能，lacal state便是这样的，仅是类组件的一个特性。
>##将`function`转成`class`
>可以分下面5个步骤将`functional`组件转成类：
>
1. 创建同名ES6 `class`拓展`React.Component`;
2. 向类中添加`reander()`方法;
3. 将`function`内容添加到`render()`中。
4. 在`render()`中用`this.props`替换掉`props`;
5. 删除剩下空的`function`声明。
>
		class Clock extends React.Component {
		  render() {
		    return (
		      <div>
		        <h1>Hello, world!</h1>
		        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
		      </div>
		    );
		  }
		}
>##向类中增加l内部state
>通过下面三步将`date`从`props`移到`state`下。
>
1. 用`this.state.date`替换掉`this.props.date`。
>
		class Clock extends React.Component {
		  render() {
		    return (
		      <div>
		        <h1>Hello, world!</h1>
		        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
		      </div>
		    );
		  }
		}
>
2. 增加类的构造函数来初始化`this.state`，
>
		class Clock extends React.Component {
		  constructor(props) {
		    super(props);
		    this.state = {date: new Date()};
		  }
>	
		  render() {
		    return (
		      <div>
		        <h1>Hello, world!</h1>
		        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
		      </div>
		    );
		  }
		}
>注:我们将`props`传递给基类构造函数，而且类组件必须调用带`props`参数的基类构造函数。
>
		constructor(props) {
		    super(props);
		    this.state = {date: new Date()};
		}
3.从`<Clock />`删除`date`属性。
>
		ReactDOM.render(
		  <Clock />,
		  document.getElementById('root')
		);
>最后完成。
>
		class Clock extends React.Component {
		  constructor(props) {
		    super(props);
		    this.state = {date: new Date()};
		  }
>		
		  render() {
		    return (
		      <div>
		        <h1>Hello, world!</h1>
		        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
		      </div>
		    );
		  }
		}
>		
		ReactDOM.render(
		  <Clock />,
		  document.getElementById('root')
		);
>下一章，我将介绍使用`clock`组件自己的定时器更新时间。