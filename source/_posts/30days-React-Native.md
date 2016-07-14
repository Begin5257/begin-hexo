title: 30days-React-Native
date: 2016-07-01 15:01:36
categories: 归纳整理 #文章文类
tags: [React-Native] #文章标签，多于一项时用这种格式
---
#### 准备工作
```
1. npm install -g react-native-cli
2. react-native init YourProjectName
3. XCode 中打开刚刚创建的工程-AwesomeProject/ios/AwesomeProject.xcodeproj
4. run
5. 在index.ios.js中进行修改
```
#### flex布局

```css
display: flex; //块级伸缩容器
display: inline-flex; //行内级伸缩容器

flex-direction: row; //水平方向，从左到右
flex-direction: reverse; //水平方向，从右到左
flex-direction: column; //垂直方向，从上到下
flex-direction: column-reverse; //垂直方向，从下到上

flex-wrap: nowrap; //默认值，不换行
flex-wrap: wrap; //允许换行
flex-wrap: wrap-reverse; //允许换行，若水平轴为主轴，则从下到上

flex-flow: row nowrap;
//伸缩项目在主轴上的对齐方式
justify-content: flex-start; //默认值，从主轴起始位置靠齐
justify-content: flex-end; //从主轴线结束位置靠齐
justify-content: center;
justify-content: space-between; //均匀分布在主轴，中间有空格
justify-content: space-around; //同上，但是两边各会保留一半空间
//伸缩项目在交叉轴上的对齐方式
align-items: flex-start; //交叉轴起始位置
align-items: flex-end;
align-items: center;
align-items: baseline; //根据基线对齐
align-items: stretch; //交叉轴方向拉伸至整个容器
//伸缩项目换行后在交叉轴上的对齐方式
align-content: flex-start;
align-content: flex-end;
align-content: center;
align-content: space-between; //伸缩项目在交叉轴中平均分布
align-content: space-around; //同上，但在两边各有一半空间
align-content: strectch; //在交叉轴延展以占用剩余空间

order: -1; //定义项目的排列顺序
flex-grow: 2; //定义伸缩项目的放大比例
flex-shrink: 3; //定义伸缩项目的收缩能力
flex-basis: 100px; //定义伸缩项目的基准值
flex: none | flex-grow flex-shrink flex-basis
```

在react-native中支持flexbox

```css
alignItems: flex-start | flex-end | center | stretch
alignSelf: auto | flex-start | flex-end | center | strecth
flex: number;
flexDirection: row | column
flexWrap: wrap | nowrap
justifyContent: flex-start | flex-end | center | space-between | space-around
```
#### 克隆项目

```
git clone https://github.com/fangwei716/30-days-of-react-native.git
git checkout RN@0.25
react-native-vector-icons
需要手动将字体添加到Xcode的项目中
首先将node_modules/react-native-vector-icons中的Fonts拖拽到Xocde中
编辑 Info.plist 添加你需要的字体
```
#### index.ios.js
1. API
    - ***AppRegistry是 JS 运行所有 React Native 应用的入口。***
      应用的根组件应当通过AppRegistry.registerComponent方法注册自己，然后原生系统才可以加载应用的代码包并且在启动完成之后通过调用AppRegistry.runApplication来真正运行应用。
    - ***TouchableHighlight 当按下的时候，封装的视图的不透明度会降低***
      同时会有一个底层的颜色透过而被用户看到，使得视图变暗或变亮。
```
renderButton: function() {
  return (
    <TouchableHighlight onPress={this._onPressButton}>
      <Image
        style={styles.button}
        source={require('./button.png')}
      />
    </TouchableHighlight>
  );
},
//TouchableHighlight只支持一个子节点
```
    - ***NavigatorIOS 包装了UIKit的导航功能，可以使用左划功能来返回上一界面***
- 路由
  ```
//一个路由是用于描述导航器中一页的对象。
render: function() {
    return (
      < NavigatorIOS
        initialRoute={{
          component: MyView,
          title: 'My View Title',
          passProps: { myProp: 'foo' },
        }}
      />
    );
}
//现在 MyView 会被导航器渲染出来。它可以通过route
属性获得对应的路由对象，导航器本身，还有所有passProps
中传递的属性。
  ```
- 导航器
  ```
var MyView = React.createClass({
    _handleBackButtonPress: function() {
          this.props.navigator.pop();
    },
    _handleNextButtonPress: function() {
          this.props.navigator.push(nextRoute);
   },
  ...
});
//一个导航器对象包括如下函数:
//1. push( route ) - 导航器跳转到一个新的路由
//2. pop() - 回到上一页
  ```

#### day1-计时器
一个IOS系统定时APP，功能与系统定时器一致。
![](https://raw.githubusercontent.com/fangwei716/ThirtyDaysOfReactNative/screenshots/screenshot/day1.gif)

将页面分为时间显示部分，控制部分，显示计次共三个部分。
每个部分独立渲染组件和样式。
实现的功能有：启动定时器，计次，停止，复位。

```javascript
//时间控制部分
this.setState({
  currentTime: (new Date()).getTime()
})
//当前时间 = 累加时间 + 当前时间 - 开始计时时间
countingTime = this.state.timeAccumulation + this.state.currentTime - this.state.initialTime;
//换算成时，分，秒
minute = Math.floor(countingTime/(60*1000));
second = Math.floor((countingTime-60000*minute)/1000);
milSecond = Math.floor((countingTime%1000)/10);
seccountingTime = countingTime - this.state.recordTime;
secminute = Math.floor(seccountingTime/(60*1000));
//这个地方原来的作者写错了6000，在git上提了issue
secsecond = Math.floor((seccountingTime-60000*secminute)/1000);
secmilSecond = Math.floor((seccountingTime%1000)/10);
//时，分，秒小于10则补零
this.setState({
  totalTime: (minute<10? "0"+minute:minute)+":"+(second<10? "0"+second:second)+"."+(milSecond<10? "0"+milSecond:milSecond),
  sectionTime: (secminute<10? "0"+secminute:secminute)+":"+(secsecond<10? "0"+secsecond:secsecond)+"."+(secmilSecond<10? "0"+secmilSecond:secmilSecond),
})
```

#### day2-天气预报

一个IOS系统的天气app，数据固定

![](https://raw.githubusercontent.com/fangwei716/ThirtyDaysOfReactNative/screenshots/screenshot/day2.gif)

这一部分比较有难度的是对天气数据的展示处理。

以及滑动时的状态变化。

```javascript
static propTypes = {
  back: React.PropTypes.func.isRequired,
};

constructor(props) {
  super(props)
  this.state = {
    weather: weatherData,
  }
}

componentDidMount() {
  StatusBar.setBarStyle(1);
}

_back() {
  this.props.back();
}
```

#### day3-Twitter开场动画

![](https://raw.githubusercontent.com/fangwei716/ThirtyDaysOfReactNative/screenshots/screenshot/day3.gif)

动画实现的思路是将中间的小图标放大，

```javascript
componentDidMount() {
    Animated.timing(
       this.state.transformAnim,
       {toValue: 50,
        duration: 1200,
        delay:2000,
        easing: Easing.elastic(2),
      },
    ).start();
    Animated.timing(
       this.state.opacityAnim,
       {toValue: 0,
        duration: 800,
        easing: Easing.elastic(1),
        delay:2200,
      },
     ).start();
    setTimeout(() => {
      this.props.hideThis();
    }, 3300);
  }
```

以及下拉刷新状态的控制

```javascript
constructor() {
    super();
    this.state = {
      isRefreshing: false,
    };
  }

  _onRefresh() {
    this.setState({
      isRefreshing: true,
    });
    setTimeout(() => {
      this.setState({
        isRefreshing: false,
      });
    }, 1000);
  }
```

