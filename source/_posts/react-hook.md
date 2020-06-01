---
title: react hook笔记
date: 2020-05-30 23:34:37
tags:
---
> 阅读[React Hooks 最佳实践](https://juejin.im/post/5ec7372cf265da76de5cd0c9?utm_source=gold_browser_extension)笔记

1. 每一帧拥有独立的变量
class和函数的对比：
``` bash
function Example(props) {
    const { count } = props;
    const handleClick = () => {
        setTimeout(() => {
            alert(count);
        }, 3000);
    };
    return (
        <div>
            <p>{count}</p>
            <button onClick={handleClick}>Alert Count</button>
        </div>
    );
}

class Example2 extends Component {
    handleClick = () => {
        setTimeout(() => {
            alert(this.props.count);
        }, 3000);
    };

    render() {
        return (
            <div>
                <h2>Example2</h2>
                <p>{this.props.count}</p>
                <button onClick={this.handleClick}>Alert Count</button>
            </div>
        );
    }
}

```
单击按钮3秒后弹出的count值 和显示的值不一致，可以看成闭包，单击那刻的count将保留不被释放，直到3秒后弹出显示，这时count已经不再是单击那刻的值了。

在 class 组件中，我们是从 this 中获取到的 props.count。this 是固定指向同一个组件实例的。在 3 秒的延时器生效后，组件重新进行了渲染，this.props 也发生了改变。当延时的回调函数执行时，读取到的 this.props 是当前组件最新的属性值。

2. 使用useRef获取过去或未来帧中的值
 ```bash
const refContainer = useRef(initialValue);
 ```
 在组件的第一帧中，refContainer.current 将被赋予初始值 initialValue，之后便不再发生变化。但你可以自己去设置它的值。设置它的值不会重新触发 render 函数。
对于 useEffect 来说，执行的时机是完成所有的 DOM 变更并让浏览器渲染页面后，而 useLayoutEffect 和 class 组件中 componentDidMount, componentDidUpdate一致——在 React 完成 DOM 更新后马上同步调用，会阻塞页面渲染。
如果 useEffect 没有传入第二个参数，那么第一个参数传入的 effect 函数在每次 render 函数执行是都是独立的。每个 effect 函数中捕获的 props 或 state 都来自于那一次的 render 函数。

 3. 每一帧可以拥有独立的 Effects
对于 useEffect 来说，执行的时机是完成所有的 DOM 变更并让浏览器渲染页面后，而 useLayoutEffect 和 class 组件中 componentDidMount, componentDidUpdate一致——在 React 完成 DOM 更新后马上同步调用，会阻塞页面渲染。

如果 useEffect 没有传入第二个参数，那么第一个参数传入的 effect 函数在每次 render 函数执行是都是独立的。每个 effect 函数中捕获的 props 或 state 都来自于那一次的 render 函数。

4. 使用 useMemo/useCallback
```bash
const data = useMemo(() => ({
    a,
    b,
    c,
    d: 'xxx'
}), [a, b, c]);

// 可以用 useCallback 代替
const fn = useMemo(() => () => {
    // do something
}, [a, b]);

const memoComponentsA = useMemo(() => (
    <ComponentsA {...someProps} />
), [someProps]);
```
useMemo 的含义是，通过一些变量计算得到新的值。通过把这些变量加入依赖 deps，当 deps 中的值均未发生变化时，跳过这次计算。useMemo 中传入的函数，将在 render 函数调用过程被同步调用。
可以使用 useMemo 缓存一些相对耗时的计算。

除此以外，useMemo 也非常适合用于存储引用类型的数据，可以传入对象字面量，匿名函数等，甚至是 React Elements。

5. 惰性初始值
```bash
const [state, setState] = useState(() => {
    const initialState = someExpensiveComputation(props);
    return initialState;
});
```
因 someExpensiveComputation 运行在一个匿名函数下，该函数当且仅当初始化时被调用，从而优化性能。

6. 受控与非受控
非受控:
```bash
useSomething = (inputCount) => {
    const [ count, setCount ] = setState(inputCount);
    setCount(inputCount);
};
```
默认不会更新，因为 useState 参数代表的是初始值，仅在 useSomething 初始时赋值给了 count state。后续 count 的状态将与 inputCount 无关。这种外部无法直接控制 state 的方式，我们称为非受控

受控：
```bash
useSomething = (inputCount) => {
    const [ count, setCount ] = setState(inputCount);
    setCount(inputCount);
};
```
