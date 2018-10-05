# Tab Navigation

**Warning: TabNavigator inside StackNavigator, can open Screen on Stack - this will open OUTSIDE TAB**

https://reactnavigation.org/docs/en/tab-navigator.html

```js
import { createBottomTabNavigator, createStackNavigator } from 'react-navigation';

export default createBottomTabNavigator({
        /* ====== Multi Stack ====== */
        Home: HomeStack,
        Settings: SettingsStack,
    },
    {
        /* ========== Custom ========== */
        navigationOptions: ({ navigation }) => ({
            tabBarIcon: ({ focused, tintColor }) => {
                const { routeName } = navigation.state;
                let iconName;
                if (routeName === 'Home') {
                    iconName = focused ? require('../images/ic_hero_focus.png') : require('../images/ic_hero.png');
                } else if (routeName === 'Settings') {
                    iconName = focused ? require('../images/ic_hero_focus.png') : require('../images/ic_hero.png');
                }

                // You can return any component that you like here! We usually use an
                // icon component from react-native-vector-icons
                return <Image source={iconName} style={{ width: 30, height: 30 }} />;
            },
        }),
        tabBarOptions: {
            activeTintColor: 'tomato',
            inactiveTintColor: 'gray',
        },
    }
);
```

## TabBar Press

```js
navigationOptions: ({ navigation }) => ({
    ...
    tabBarOnPress: ({ navigation, defaultHandler }) => {
        // ========== Run function when select ScanQR Tab ==========
        const parentNavigation = navigation.dangerouslyGetParent();
        const prevRoute = parentNavigation.state.routes[parentNavigation.state.index];
        const currRoute = navigation.state;
        
        if (currRoute.routeName === 'ScanProduct') {
        // store.dispatch(updateCameraVisible(true)); // Call Action: Show Camera

        } else {
        // store.dispatch(updateCameraVisible(false)); // Call Action: hide Camera
        }

        defaultHandler(); // action selected
    },
```

## Some Options

```js
tabBarOptions: {
  labelStyle: {
    fontSize: 12,
  },
  tabStyle: {
    width: 100,
  },
  style: {
    backgroundColor: 'blue',
  },
}
```