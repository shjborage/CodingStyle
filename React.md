# React Coding Style
> 引自 https://segmentfault.com/a/1190000003789022?_ea=380891#articleHeader3  
> [帕斯卡命名法](http://baike.baidu.com/link?url=gz8jTbJjkU1tFrpF-auLEuVd3iB_nro6n0MDLkgjQUdd_Q9jhkqAOPwp7yV5cnrrU9CftPP1YVzNICHjHQ8phq)

[1. Basic Rules](#1-basic-rules)  

[2. Component](#2-component)  
　　[2.1 Class 与 React.createClass方法](#21-class-与-react.createclass方法)  
　　[2.2 组件命名](#22-组件命名)  
　　[2.3 Declaration](#23-declaration)  
　　[2.4 Props](#24-props)

[3. JSX](#3-jsx)  
　　[3.1 Alignment](#31-alignment)  
　　[3.2 Quotes](#32-quotes)  
　　[3.3 Spacing](#33-spacing)  
　　[3.4 多段](#34-多段)

[4. Methods](#4-methods)  
　　[4.1 Naming](#41-naming)


## 1. Basic Rules
[建议] 每个文件中只包含一个 `React` 组件  
[建议] 尽可能地使用 `JSX` 语法  
[强制] 除非不用 `JSX` 语法创建一个应用，否则不要使用 `React.createElement` 方法。  

## 2. Component
### 2.1 Class 与 React.createClass方法  
[建议] 尽可能地使用ES6中的类的语法，除非有特殊的对于 `Mixin` 的需求  

示例：
```
// bad
const Listing = React.createClass({
  render() {
    return <div />;
  }
});

// good
class Listing extends React.Component {
  render() {
    return <div />;
  }
}
```

### 2.2 组件命名
[强制] 扩展名：使用 `.jsx`作为 `React` 组件的扩展名
[强制] 文件名：使用帕斯卡命名法命名文件，譬如 `ReservationCard.jsx`
[强制] 引用命名：使用帕斯卡命名法命名组件和camelCase命名实例  

示例：
```
// bad
const reservationCard = require('./ReservationCard');

// good
const ReservationCard = require('./ReservationCard');

// bad
const ReservationItem = <ReservationCard />;

// good
const reservationItem = <ReservationCard />;
```

### 2.3 Declaration
[强制] 不要使用displayName来命名组件，而使用引用
示例：
```
// bad
export default React.createClass({
  displayName: 'ReservationCard',
  // stuff goes here
});

// good
export default class ReservationCard extends React.Component {
}
```

### 2.4 Props
[强制] 对于Props的命名使用camelCase  

示例：
```
// bad
<Foo
  UserName="hello"
  phone_number={12345678}
/>

// good
<Foo
  userName="hello"
  phoneNumber={12345678}
/>
```

[建议] 将Props或者State的声明写在类外  

示例：
```
import React, { Component, PropTypes } from 'react';

const propTypes = {
  id: PropTypes.number.isRequired,
  url: PropTypes.string.isRequired,
  text: PropTypes.string,
};

const defaultProps = {
  text: 'Hello World',
};

export default class Link extends Component {
  static methodsAreOk() {
    return true;
  }

  render() {
    return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>
  }
}

Link.propTypes = propTypes;
Link.defaultProps = defaultProps;
```


## 3. JSX
### 3.1 Alignment  
示例：
```
// bad
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />

// good
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>

// if props fit in one line then keep it on the same line
<Foo bar="bar" />

// children get indented normally
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
>
  <Spazz />
</Foo>
```

### 3.2 Quotes  
[强制] 对于JSX的属性用双引号表示，对于其他属性，用单引号表示  

示例：
```
// bad
<Foo bar='bar' />

// good
<Foo bar="bar" />

// bad
<Foo style={{ left: "20px" }} />

// good
<Foo style={{ left: '20px' }} />
```

### 3.3 Spacing
[强制] 在自闭合的标签中仅使用单空格  

示例：
```
// bad
<Foo/>

// very bad
<Foo                 />

// bad
<Foo
 />

// good
<Foo />
```

### 3.4 多段
[强制] 当JSX包含多行代码时，将它们包含在小括号中  

示例：
```
/// bad
render() {
  return <MyComponent className="long body" foo="bar">
           <MyChild />
         </MyComponent>;
}

// good
render() {
  return (
    <MyComponent className="long body" foo="bar">
      <MyChild />
    </MyComponent>
  );
}

// good, when single line
render() {
  const body = <div>hello</div>;
  return <MyComponent>{body}</MyComponent>;
}
```

## 4. Methods
### 4.1 Naming
[强制] 对于一个React组件的内部方法，不要使用下划线作为前缀  

示例：
```
// bad
React.createClass({
  _onClickSubmit() {
    // do stuff
  }

  // other stuff
});

// good
class extends React.Component {
  onClickSubmit() {
    // do stuff
  }

  // other stuff
});
```
