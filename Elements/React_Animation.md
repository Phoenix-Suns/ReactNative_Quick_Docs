```js
export default class ComponentTest extends Component<Props> {

  constructor () {
  	super()
    this.animatedValue = new Animated.Value(0)
  }

  stateRotate = () => {
    animatedValue = new Animated.Value(0)

    // First set up animation 
    Animated.timing(
        this.animatedValue,
        {
          toValue: 1,
          duration: 30000,
          easing: Easing.linear
        }
      ).start()
  }

  render() {
    const to = 360 * 3 + 90;
    // Second interpolate beginning and end values (in this case 0 and 1)
    const spin = this.animatedValue.interpolate({
      inputRange: [0, 1],
      outputRange: ['0deg', to+'deg']
    });

    return (
      <View style={styles.container}>
        <Button title='Start'
          onPress={this.stateRotate} 
        />
        <Animated.Image
          style={{transform: [{rotate: spin}] }}
          source={require('./images/capture.png')} />
      </View>
    );
  }
}
```