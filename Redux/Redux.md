# Redux Observable

<!-- TOC -->

- [Redux Observable](#redux-observable)
    - [Nguyên tắc](#nguyên-tắc)
        - [3 nguyên tắc của Redux](#3-nguyên-tắc-của-redux)
        - [Cách thức hoạt động](#cách-thức-hoạt-động)
            - [Action:](#action)
            - [Reducers](#reducers)
            - [Store](#store)
    - [Cài đặt](#cài-đặt)
    - [Ví dụ](#ví-dụ)
        - [Mô tả thư mục](#mô-tả-thư-mục)
        - [Code](#code)
            - [Cài đặt trong App](#cài-đặt-trong-app)
            - [Cài đặt Store](#cài-đặt-store)
            - [Component Gọi Action để sử dụng](#component-gọi-action-để-sử-dụng)
            - [Action](#action)
            - [Reducer](#reducer)
            - [Middleware - Redux Observable: to Get Data](#middleware---redux-observable-to-get-data)
    - [Redux - Thunk](#redux---thunk)
        - [Store](#store-1)
        - [Action](#action-1)
    - [Call Action Outside Component](#call-action-outside-component)

<!-- /TOC -->

## Nguyên tắc

### 3 nguyên tắc của Redux

- Single source of truth: State của toàn bộ ứng dụng được lưu trong trong 1 store duy nhất là 1 Object mô hình tree.
- State is read-only: Chỉ có 1 cách duy nhất để thay đổi state đó là tạo ra một action (là 1 object mô tả những gì xảy ra)
- Changes are made with pure functions: Để chỉ rõ state tree được thay đổi bởi 1 action bạn phải viết pure reducers

### Cách thức hoạt động

![Redux Operation](../images/redux_operation.gif)

#### Action: 

Định nghĩa Giá trị được Luân chuyển, Mô tả hành động
Mỗi action là 1 Fure Object, 2 thuộc tính:

```
{
  type: "KIEU_ACTION",
  payload: //tham số
}
```

#### Reducers

Chuyển đổi giá trị, nhận vào State cũ + Action => Trả về State mới

```
(previousState, action) => newState
```

#### Store

Lưu trữ State toàn ứng dụng

## Cài đặt

npm install --save redux
npm install --save react-redux
npm install --save redux-observable
npm install --save rxjs

## Ví dụ

### Mô tả thư mục

- App.js
- src
- - redux
- - AppStore.js
- - action.js
- - AppReducers
- Constant.js
- TestScene.js  // Component for Showing

### Code

#### Cài đặt trong App

```js
// Config trong App.js
class App extends Component {

  render() {
    return (
      <Provider store={AppStore()}>
        <TestScene />
      </Provider>
    );
  }
}
export default App;
```

#### Cài đặt Store

```js
// Tạo Store: src/redux/AppStore.js
import { createStore, applyMiddleware, compose } from 'redux'
import { createEpicMiddleware } from 'redux-observable'
import { retry } from 'rxjs/operator/retry';
import AppReducers from './AppReducers'
import fetchUserEpic from './epic'

// Kết hợp nhiều Middleware lại
const epicMiddleware = createEpicMiddleware(fetchUserEpic); // sẽ Tạo sau

const AppStore = () => {
  return createStore(
    AppReducers(),  // Sẽ tạo sau
    applyMiddleware(epicMiddleware)
    )
}
export default AppStore;
```

#### Component Gọi Action để sử dụng

```js
...
import { connect } from "react-redux";
import { bindActionCreators } from "redux";
import { getUserRequest } from "./redux/UserAction";

class TestScene extends React.Component {

    _onGetPress = () => {
        this.props.getUserRequest('luunghiatran');  // Gọi Action trong Store
    }

    render () {
        const {loading, error, data } = this.props;

        return (
            <View>
                { loading ?
                    <Text>Loading</Text> :
                    <Button title="Get" onPress={this._onGetPress}></Button>
                }
                <Text style={{color:'red'}}>{error}</Text>
                <Text>{ data ? data.avatar_url : "DATA HERE"}</Text>
            </View>
        )
    }
}

// Chuyển State Thành Props để render
const mapStateToProps = (state) => {
    return {
        loading: state.UserReducer.loading,
        error: state.UserReducer.error,
        data: state.UserReducer.data
    };
}
  
// Khai báo Action sử dụng
function dispatchToProps(dispatch) {
    return bindActionCreators({getUserRequest}, dispatch);
}

// Kết nối component và Store, kết quả trả về trong mapStateToProps
export default connect(mapStateToProps, dispatchToProps)(TestScene);
```

#### Action

```js
//src/redux/UserAction.js
// Tạo Action: Để lưu trữ giá trị luân chuyển
// Redux Observable
export const getUserRequest = (search) => ({type: 'FETCHING_USER_REQUEST', payload: search})
export const getUserSuccess = (data) => ({ type: 'FETCHING_USER_SUCCESS', payload: data })
export const getUserFailure = (error) => ({ type: 'FETCHING_USER_FAILURE', payload: error, error: true })
```

#### Reducer

```js
// Tạo Reducer chuyển đổi State
// Reducer để get Data
export const UserReducer = (state = INITIAL_STATE, action) => {
    switch (action.type) {
        case 'FETCHING_USER_REQUEST':
            return { ...state, loading: true  };
        case 'FETCHING_USER_SUCCESS':
            return { ...state, loading: false, data: action.payload };
        case 'FETCHING_USER_FAILURE':
            return { ...state, loading: false };
        default:
            return state;
    }
};


// File: src/redux/AppReducers.js
...
import { combineReducers } from "redux";

// Kết hợp nhiều reducers lại
const AppReducers = () => {
    return combineReducers({
        UserReducer,
    })
}
export default AppReducers;
```

#### Middleware - Redux Observable: to Get Data

```js
// File: src/redux/epic.js
// Tạo Epic (Middleware Observable), để get Data
// Redux Observable
import { getUserSuccess, getUserFailure } from './actions'
import 'rxjs'
import { Observable } from 'rxjs/Observable'

const fetchUser = (userName) => {
  //https://api.github.com/users/userName
  const request = fetch(`https://api.github.com/users/${userName}` ,
  {
    method: 'GET',
    headers: "{ 'Accept': 'application/json', 'Content-Type': 'application/json' }"
  })
  .then(response => response.json());
  return request;
}

const fetchUserEpic = action$ =>
  action$
  .ofType('FETCHING_USER_REQUEST')
  .debounceTime(500) // Delay
  .switchMap(action => Observable.from(fetchUser(action.payload))
    .map(response => getUserSuccess(response))
    .catch(error => Observable.of(getUserFailure(error))
    )
  );
export default fetchUserEpic;
```

## Redux - Thunk

### Store

```js
...
import { createStore, applyMiddleware, compose } from 'redux';
import ReduxThunk from 'redux-thunk';

const epicMiddleware = createEpicMiddleware(fetchUserEpic) // Redux Observable

const AppStore = () => {
  return createStore(
    AppReducers(),
    applyMiddleware(ReduxThunk) // Redux Thunk
    //applyMiddleware(epicMiddleware) // Redux Observable
    );
}

export default AppStore;
```

### Action

```js
// Redux Thunk
export const getUserRequest = (search) => {
    return(dispatch) => {
        dispatch({ type: FETCHING_USER_REQUEST, payload: search });

        var url = `https://api.github.com/users/${search}`;
        return request = fetch(url, {
            method: 'GET',
            headers: "{ 'Accept': 'application/json', 'Content-Type': 'application/json' }"
            })
            .then(response => // Return Promise
                response.json().then( data => 
                    userSuccess(dispatch, data)
                )
            )
            .catch(error => userFailure(dispatch, error));
    };
};

const userSuccess = (dispatch, response) => { 
    dispatch ({ type: FETCHING_USER_SUCCESS, payload: response });
}
const userFailure = (dispatch, error) => {
    dispatch ({ type: FETCHING_USER_FAILURE, payload: error, error: true })
}
```

## Call Action Outside Component

```java
AppStore.dispatch(Action(params));
```

---
**Copy:**
https://redux.js.org/basics/exampletodolist
https://insights.innovatube.com/redux-th%E1%BA%ADt-l%C3%A0-%C4%91%C6%A1n-gi%E1%BA%A3n-ph%E1%BA%A7n-cu%E1%BB%91i-4155b1cfed03