# React Native cơ bản 1

## Khái niệm cơ bản

### Props: Data truyền vào Component

- Không thể thay đổi trong Component

![props](basic_1_props.png)

```js
// Truyền Props vào để Hiển thị tên

import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

// Create Greeting (Show text)
class Greeting extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Text>Hello {this.props.name}!</Text>
      </View>
    );
  }
}

// Using Greeting (to show array text)
export default class LotsOfGreetings extends Component {
  render() {
    // --- Gọi 3 component Greeting với tham số Name ---
    return (
      <View style={{alignItems: 'center', top: 50}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => LotsOfGreetings);
```

### State: Data thay đổi trong Component

- thường khởi tạo trong Construct
- đổi data: setSate
  
```js
// Tạo Component Blink (chữ chớp chớp)
import React, { Component } from 'react';
import { Text, View } from 'react-native';

class Blink extends Component {

  componentDidMount(){
    // Toggle the state every second
    setInterval(() => (
      this.setState(previousState => (
        { isShowingText: !previousState.isShowingText }
      ))
    ), 1000);
  }

  //state object
  state = { isShowingText: true };

  render() {
    // hide Text
    if (!this.state.isShowingText) {
      return null;
    }

    // show Text
    return (
      <Text>{this.props.text}</Text>
    );
  }
}
```

```js
// Using Component Blink
export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}
```

### Style Component: Trang trí Component

![style](basic_1_style.png)

```js
import React, { Component } from 'react';
import { StyleSheet, Text, View } from 'react-native';

const styles = StyleSheet.create({
  bigBlue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});

export default class LotsOfStyles extends Component {
  render() {
    return (
      <View>
        <Text style={styles.red}>just red</Text>
        <Text style={styles.bigBlue}>just bigBlue</Text>
        <Text style={[styles.bigBlue, styles.red]}>bigBlue, then red</Text>
        <Text style={[styles.red, styles.bigBlue]}>red, then bigBlue</Text>
        <Text style={{color: 'green', fontSize: 30}}>green text</Text>
      </View>
    );
  }
}
```

- Note:
  - Style trực tiếp: style={{color: 'green', fontSize: 30}}
  - Gọi Style: style={[styles.bigBlue, styles.red]}

---

## References

- <https://facebook.github.io/react-native/docs/getting-started>
- <https://viblo.asia/p/hoc-react-native-tu-co-ban-den-nang-cao-phan-2-khai-niem-co-ban-trong-react-native-va-1-so-chia-se-ca-nhan-RQqKLvN6l7z>
  