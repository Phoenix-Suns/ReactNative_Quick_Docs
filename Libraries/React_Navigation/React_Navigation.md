# Thư viện Điều hướng - React Navigation

<https://reactnavigation.org/>
<https://reactnavigation.org/docs/en/getting-started.html>

- [Thư viện Điều hướng - React Navigation](#th%c6%b0-vi%e1%bb%87n-%c4%90i%e1%bb%81u-h%c6%b0%e1%bb%9bng---react-navigation)
  - [Setup](#setup)
  - [Simple Start](#simple-start)
  - [Navigation - điều hướng](#navigation---%c4%91i%e1%bb%81u-h%c6%b0%e1%bb%9bng)
  - [Params - Truyền Data khi điều hướng](#params---truy%e1%bb%81n-data-khi-%c4%91i%e1%bb%81u-h%c6%b0%e1%bb%9bng)
    - [Master to Detail](#master-to-detail)
    - [Detail callback Master](#detail-callback-master)
  - [navigationOptions - Tùy chỉnh Navigation](#navigationoptions---t%c3%b9y-ch%e1%bb%89nh-navigation)
    - [Tùy Chỉnh trong Component](#t%c3%b9y-ch%e1%bb%89nh-trong-component)
    - [Tùy chỉnh trong createStack (App.js)](#t%c3%b9y-ch%e1%bb%89nh-trong-createstack-appjs)
    - [1 số thuộc tính](#1-s%e1%bb%91-thu%e1%bb%99c-t%c3%adnh)

## Setup

yarn add react-navigation
or
npm install --save react-navigation

npm install react-native-gesture-handler react-native-reanimated

## Simple Start

```js
// App.js
import { createStackNavigator } from 'react-navigation';

const RootStack = createStackNavigator({
  {
    // HomeScreen Component
    Home: HomeScreen,
    // Detail Screen Component
    Detail: DetailScreen
  },
  {
    initialRouteName: 'Home',   // First Screen is "Home"
  }
});

export default class App extends React.Component {
  render() {
    return <RootStack />;
  }
}
```

## Navigation - điều hướng

<https://reactnavigation.org/docs/en/stack-actions.html>

```java
this.props.navigation.navigate('Details')   // Goto Details Screen
this.props.navigation.goBack()
this.props.navigation.push('Details')       // Go to Detail Again (push Detail to Stack)
```

## Params - Truyền Data khi điều hướng

<https://reactnavigation.org/docs/en/navigation-prop.html>
<https://reactnavigation.org/docs/en/navigation-actions.html>

### Master to Detail

```js
// MasterScreen Component
this.props.navigation.navigate('Details', {
    textParam1: 'write some thing',     // Send String Param to Detail Screen
}

// DetailScreen Component
render() {
    /* Receive Params */
    const { navigation } = this.props;
    const textParam1 = navigation.getParam('textParam1', 'default value');
    //...
}
```

### Detail callback Master

```js
// MasterScreen Component
this.props.navigation.navigate('Details', {
    updateId: this.updateId.bind(this), // Send Function, Detail Callback
}

// DetailScreen Component
onPress={() => {
    this.props.navigation.state.params.updateId('123'); // Set/Call UpdateId on MasterScreen
}
```

## navigationOptions - Tùy chỉnh Navigation

<https://reactnavigation.org/docs/en/stack-navigator.html>

### Tùy Chỉnh trong Component

```js
// DetailsScreen.js
class DetailsScreen extends React.Component {

  // ==========================================
  // === Config Header bar, get param -> set title ===
  static navigationOptions = ({ navigation }) => {
    const params = navigation.state.params || {};
    return {
      title: 'Title is ' + navigation.getParam('textParam1', 'NO-ID'),
      headerRight: (
        // ========= Button On Header ============
        // Call Event on Component
        <Button onPress={navigation.getParam('increaseCount')}/>
      )};
  };
  //...

  // Binding Header Button Event to Component fuction: increaseCount is  this._increaseCount
   componentDidMount() {
    this.props.navigation.setParams({ increaseCount: this._increaseCount });
  }

  _increaseCount = () => {
    this.setState({ count: this.state.count + 1 });
  };
}
```

### Tùy chỉnh trong createStack (App.js)

```js
const RootStack = createStackNavigator({
  // For each screen that you can navigate to, create a new entry like this:
  Details: {
    // `DetailScreen` is a React component that will be the main content of the screen.
    screen: DetailScreen,

    // ==========================================
    // === Optional: Override the `navigationOptions` for the screen ===
    navigationOptions: ({ navigation }) => ({
      title: `${navigation.state.params.textParam1}'s Profile'`,
    }),
  },
  //...MyOtherRoutes,
}, {

  initialRouteName: 'Home',

  //===== Hide Header =========
  /* mode: 'modal',
  headerMode: 'none', */

  // ==========================================
  /* === The config header ALL Component === */
  navigationOptions: {
    //...
  }
});
```

### 1 số thuộc tính

```js
navigationOptions: {
  headerStyle: {
      backgroundColor: '#f4511e',
  },
  headerTintColor: '#fff',
  headerTitleStyle: {
      fontWeight: 'bold',
  },
  title: ...
  headerTitle: <View />
  headerRight: <View />
}
```

---
