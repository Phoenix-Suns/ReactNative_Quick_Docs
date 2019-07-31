# Networking: Lấy dữ liệu từ API

```js
function getMoviesFromApiAsync() {
  return fetch('https://facebook.github.io/react-native/movies.json')
    .then((response) => response.json())
    .then((responseJson) => {

      //return responseJson.movies;
      this.setState({
          dataSource: responseJson.movies,
        });

    })
    .catch((error) => {
      console.error(error);
    });
}
```

---

- <https://facebook.github.io/react-native/docs/network>
