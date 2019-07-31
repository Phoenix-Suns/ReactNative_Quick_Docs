# FlatList - Section Hiển thị list view

## Ghi nhớ

```js
<FlatList
    data={this.state.flatListData}
    renderItem={({item}) => <Text>{item.key}</Text>}
/>
```

```js
<SectionList
    sections={this.state.sectionListData}
    renderItem={({item}) => <Text>{item}</Text>}
    renderSectionHeader={({section}) => <Text>{section.title}</Text>}
    keyExtractor={(item, index) => index}
/>
```

## FlatList - Hiển thị list bình thường

![flat list](flatlist.png)

```js
constructor(props) {
    super(props);
    this.state = {
      flatListData: [
            {key: 'Devin'},
            {key: 'Jackson'},
            {key: 'James'},
            {key: 'Joel'},
            {key: 'John'},
            {key: 'Jillian'},
            {key: 'Jimmy'},
            {key: 'Julie'},
          ]
    };
  }

render() {
    return (
      <View style={styles.container}>
        <FlatList
          data={this.state.flatListData}
          renderItem={({item}) => <Text style={styles.item}>{item.key}</Text>}
        />
      </View>
    );
  }
```

## SectionList - Hiển thị list theo section

![section list](sectionlist.jpg)

```js
constructor(props) {
    super(props);
    this.state = {
      sectionListData: [
        {
          title: "D",
          data: ["Devin"]
        },
        {
          title: "J",
          data: ["Jackson", "James", "Jillian", "Jimmy", "Joel", "John", "Julie"]
        }
      ]
    };
  }
  
  render() {
    return (
      <View style={styles.container}>
        <SectionList
          sections={this.state.sectionListData}
          renderItem={({item}) => <Text style={styles.item}>{item}</Text>}
          renderSectionHeader={({section}) => <Text style={styles.sectionHeader}>{section.title}</Text>}
          keyExtractor={(item, index) => index}
        />
      </View>
    );
  }
```

---
