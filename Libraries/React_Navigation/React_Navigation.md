# Thư viện Điều hướng - React Navigation

https://reactnavigation.org/

<!-- TOC -->

- [Thư viện Điều hướng - React Navigation](#thư-viện-điều-hướng---react-navigation)
    - [Setup](#setup)
    - [Simple Start](#simple-start)
    - [Navigation - điều hướng](#navigation---điều-hướng)
    - [Params - Truyền Tham số khi điều hướng](#params---truyền-tham-số-khi-điều-hướng)
    - [Navigation Option - Tùy chọn/ Cài đặt khi điều hướng](#navigation-option---tùy-chọn-cài-đặt-khi-điều-hướng)
        - [Set on Component or on createStack](#set-on-component-or-on-createstack)
        - [1 số thuộc tính:](#1-số-thuộc-tính)

<!-- /TOC -->

## Setup

yarn add react-navigation
or
npm install --save react-navigation

## Simple Start

```js
const RootStack = createStackNavigator({
  Home: {
    screen: HomeScreen // Component HomeScreen
  },
  {
    initialRouteName: 'Home',   // First Screen
  }
});

export default class App extends React.Component {
  render() {
    return <RootStack />;
  }
}
```

## Navigation - điều hướng
https://reactnavigation.org/docs/en/stack-actions.html

```java
this.props.navigation.navigate('Details')   // Goto Details Screen
this.props.navigation.goBack()
this.props.navigation.push('Details')       // Go to Detail Again (push Detail to Stack)
```

## Params - Truyền Tham số khi điều hướng
https://reactnavigation.org/docs/en/navigation-prop.html
https://reactnavigation.org/docs/en/navigation-actions.html

```js
// MasterScreen
this.props.navigation.navigate('Details', {
    textParam1: 'write some thing',     // Send String Param to Detail Screen
    updateId: this.updateId.bind(this), // Send Function, Detail Callback
}

// Details: DetailScreen
render() {
    /* Receive Params */
    const { navigation } = this.props;
    const textParam1 = navigation.getParam('textParam1', 'default value');
    //...
}

onPress={() => {
    this.props.navigation.state.params.updateId('123'); // Set/Call UpdateId on MasterScreen
}
```

## Navigation Option - Tùy chọn/ Cài đặt khi điều hướng

https://reactnavigation.org/docs/en/stack-navigator.html

### Set on Component or on createStack

```js
// === Set on Component ===
class DetailsScreen extends React.Component {
  // Config Header bar, get param -> set title
  static navigationOptions = ({ navigation }) => {
    const params = navigation.state.params || {};
    return {
      title: 'Title is ' + navigation.getParam('textParam1', 'NO-ID'),
      headerRight: (
        // ========= Button On Header ============
        <Button onPress={navigation.getParam('increaseCount')}  // Call Event on Component />
      )};
  };
  //...

  // Set Event into Params
   componentDidMount() {
    this.props.navigation.setParams({ increaseCount: this._increaseCount });
  }
}

// === Set on CreateStack ===
createStackNavigator({
  // For each screen that you can navigate to, create a new entry like this:
  Details: {
    // `DetailScreen` is a React component that will be the main content of the screen.
    screen: DetailScreen,

    // Optional: Override the `navigationOptions` for the screen
    navigationOptions: ({ navigation }) => ({
      title: `${navigation.state.params.textParam1}'s Profile'`,
    }),
  },
  ...MyOtherRoutes,
}, {

  initialRouteName: 'Home',

  // ========= Header All Stack ==================
  //===== Hide Header =========
  /* mode: 'modal',
  headerMode: 'none', */

  /* The header config ALL */
  navigationOptions: { ... }
});
```

### 1 số thuộc tính:

```js
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
```

