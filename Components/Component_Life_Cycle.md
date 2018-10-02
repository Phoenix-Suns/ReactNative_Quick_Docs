# Component Life Cycle - Vòng đời Component

## Mounting - Render lần đầu

constructor
componentWillMount
render
componentDidMount

## Updating - Mỗi lần Render, sau lần đầu

componentWillReceiveProps (nextProps)
shouldComponentUpdate (nextProps, nextState, nextContext)

componentWillUpdate (nextProps, nextState)
render
componentDidUpdate (prevProps, prevState, prevContext)

## Unmounting - Component Destroy, Remove, Clean Up

componentWillUnmount


---
**Tham Khảo**
- https://medium.com/@baphemot/understanding-reactjs-component-life-cycle-823a640b3e8d
- https://viblo.asia/p/vong-doi-cua-mot-react-component-RQqKLMRzZ7z