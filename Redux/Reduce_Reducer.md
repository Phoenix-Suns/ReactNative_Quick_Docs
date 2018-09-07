# Đơn giản hóa reducer: REQUEST, SUCCESS, FAILURE

https://medium.com/stashaway-engineering/react-redux-tips-better-way-to-handle-loading-flags-in-your-reducers-afda42a804c6

<!-- TOC -->

- [Đơn giản hóa reducer: REQUEST, SUCCESS, FAILURE](#đơn-giản-hóa-reducer-request-success-failure)
    - [Mục đích rút gọn UserProducer](#mục-đích-rút-gọn-userproducer)
    - [Thực hiện](#thực-hiện)
        - [Tạo loadingReducer: xử lý **loading state**](#tạo-loadingreducer-xử-lý-loading-state)
        - [Tạo **createLoadingSelector**: convert loading state trả về, hiển thị trong View](#tạo-createloadingselector-convert-loading-state-trả-về-hiển-thị-trong-view)
    - [Áp dụng với Error State](#áp-dụng-với-error-state)

<!-- /TOC -->


## Mục đích rút gọn UserProducer

loại bỏ FETCHING_USER_REQUEST, FETCHING_USER_ERROR

Từ:

```js
export const UserProducer = (state = INITIAL_STATE, action) => {
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
```

Thành:

```js
export const UserProducer = (state = INITIAL_STATE, action) => {  
    switch(action.type) {
        case 'FETCHING_USER_SUCCESS':
            return { ...state, data: action.payload };

        default:
            return state;
        }
};
```

## Thực hiện

### Tạo loadingReducer: xử lý **loading state** 

Chỉ có Action "*_REQUEST" trả về {loading: true}

```js
// src/redux/api/loadingReducer.js
const loadingReducer = (state = {}, action) => {
    const { type } = action;
    const matches = /(.*)_(REQUEST|SUCCESS|FAILURE)/.exec(type);

    // not a *_REQUEST / *_SUCCESS /  *_FAILURE actions, so we ignore them
    if (!matches) return state;  
    
    const [, requestName, requestState] = matches;
    return {
      ...state,
      // Store whether a request is happening at the moment or not
      // e.g. will be true when receiving GET_TODOS_REQUEST
      //      and false when receiving GET_TODOS_SUCCESS / GET_TODOS_FAILURE
      [requestName]: requestState === 'REQUEST',
    };
};
export default loadingReducer;


// src/redux/AppReducers.js
const AppReducers = () => {
    return combineReducers({
        ...
        UserProducer,
        loading: loadingReducer,
        //error: errorReducer,    //Sẽ làm sau
    })
}
```

### Tạo **createLoadingSelector**: convert loading state trả về, hiển thị trong View

```js
// src/redux/selector.js
// Actions: Init Parameter, State: pass parameter
export const createLoadingSelector = (actions) => (state) => {
    // returns true only when all actions is not loading
    return actions.some(action => state.loading[action]);
};


// Sử dụng trong Component:
// src/TestScene.js
const loadingSelector = createLoadingSelector(['FETCHING_USER']);
const errorSelector = createErrorMessageSelector(['FETCHING_USER']);

const mapStateToProps = (state) => {
    var result = {
        loading: loadingSelector(state),    // Convert state thành loading
        error: errorSelector(state),        // Convert error thành error, thực hiện sau
        data: state.UserProducer.data
    };
    return result;
}
```

## Áp dụng với Error State

```js
// src/redux/api/errorReducer.js
const errorReducer = (state = {}, action) => {
    const { type, payload } = action;
    const matches = /(.*)_(REQUEST|FAILURE)/.exec(type);
  
    // not a *_REQUEST / *_FAILURE actions, so we ignore them
    if (!matches) return state;
  
    const [, requestName, requestState] = matches;
    return {
      ...state,
      // Store errorMessage
      // e.g. stores errorMessage when receiving GET_TODOS_FAILURE
      //      else clear errorMessage when receiving GET_TODOS_REQUEST
      [requestName]: requestState === 'FAILURE' ? payload : '',
    };
  };
export default errorReducer;


// src/redux/api/selectors.js
export const createErrorMessageSelector = (actions) => (state) => {
    // returns the first error messages for actions
    // * We assume when any request fails on a page that
    //   requires multiple API calls, we shows the first error

    const errors = actions.map(action => state.error[action]);
    if (errors && errors[0]) {
        return errors[0];
    }
    return '';
  };
```
