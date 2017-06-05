需要注意的点
# e.target.value
[e.target.value](http://www.imooc.com/qadetail/153498)

# this.state
组件免不了要与用户互动，React 的一大创新，就是将组件看成是一个状态机，一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染 UI 
上面代码是一个Input组件 ，他的constructor方法(构造函数)用于定义初始状态
也就是一个对象，这个对象通过this.state属性读取。
当用户点击组件，导致状态变化(触发onChange事件，执行changeHandler函数，e.target.value获取事件执行时鼠标所点击区域的那个元素的value)
his.setState 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。

# this.props vs this.state 
由于 this.props 和 this.state 都用于描述组件的特性，可能会产生混淆。一个简单的区分方法是，this.props 表示那些一旦定义，就不再改变的特性，而 this.state 是会随着用户互动而产生变化的特性。

# 表单

用户在表单填入的内容，属于用户跟组件的互动，所以不能用 this.props 读取

上面代码中，文本输入框的值，不能用 this.props.value 读取，而要定义一个 onChange 事件的回调函数，通过 event.target.value 读取用户输入的值。textarea 元素、select元素、radio元素都属于这种情况，更多介绍请参考[官方文档]()。

# this

```
    render() {
        return (
            <div>
               <input 
                    style={{width: '100%', height: '40px', fontSize: '35px'}}
                    value={this.state.value} 
                    onChange={this.changeHandler.bind(this)} 
                    onKeyUp={this.keyUpHandler.bind(this)}
                />
            </div>
        )
    }
    changeHandler(e) {
        // 实时同步数据
        this.setState({value: e.target.value})
    }

```
这里的this 指的是conponent的实例对象
调用函数对象的apply/call/bind等方法，其作用是改变函数的调用对象，他们的第一个参数就表示改变后的能 调用这个函数的对象(函数成为了第一个参数所对应的对象的方法)，this指的就是这第一个参数

详解 [戳这里](http://www.imooc.com/video/9820)
![](http://on891bjlf.bkt.clouddn.com/image/00.png)

```


var g = f.bind({a: 'test'});
function f() {
    return this.a;
}
console.log(g()); // test

```

这里调用bind后就是 {a: 'test'} 这个对象有一个为a 的属性 和为 f 的函数 