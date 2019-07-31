# Drawer - Slide Menu

<https://reactnavigation.org/docs/en/drawer-navigator.html>

## Custom Drawer

```js
export default createDrawerNavigator({
        /* ====== Multi Stack ====== */
        Home: HomeStack,    // Open stack Inside
        Settings: SettingsStack,   // Open Stack Outside
    },
    {
        //============ Custom UI ==============
        drawerWidth: 300,
        contentComponent: DrawerScreen,
        contentOptions: { ... }
    }
);
```

```js
import {NavigationActions,  DrawerActions, SafeAreaView} from 'react-navigation';

export default class DrawerScreen extends Component {
  navigateToScreen = (route) => () => {
    const navigateAction = NavigationActions.navigate({
      routeName: route
    });
    this.props.navigation.dispatch(navigateAction);
    this.props.navigation.dispatch(DrawerActions.closeDrawer())
  }

  render () {
    return (
      <ScrollView>
        <SafeAreaView style={{flex: 1}} forceInset={{ top: 'always', horizontal: 'never' }}>
          <View>
              <Button onPress={this.navigateToScreen('Settings')} />
          </View>
        </SafeAreaView>
      </ScrollView>
    );
  }
}
```

## Action - Điều hướng

```js
navigation.toggleDrawer() // Open Drawer menu
```

## Some Options

```js
contentOptions: {
  activeTintColor: '#e91e63',
  itemsContainerStyle: {
    marginVertical: 0,
  },
  iconContainerStyle: {
    opacity: 1
  }
}
```

---
