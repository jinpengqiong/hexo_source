---
title: useCallback、useMemo 分析 & 差别
date: 2021-05-06 15:25:06
tags:
---
- useCallback是根据依赖(deps)缓存第一个入参的(callback)。
- useMemo是根据依赖(deps)缓存第一个入参(callback)执行后的值。
举个🌰：
```bash
import React,{useState,memo,useMemo,useCallback} from 'react';

function SubCounter({onClick,data}){
    console.log('SubCounter render', onClick, data);
    return (
        <button onClick={onClick}>{data.number}</button>
    )
}
SubCounter = memo(SubCounter);

let oldData,oldAddClick;
export function TEST(){
    console.log('Counter render');
    const [name,setName]= useState('计数器');
    const [number,setNumber] = useState(0);
    // 父组件更新时，这里的变量和函数每次都会重新创建，那么子组件接受到的属性每次都会认为是新的
    // 所以子组件也会随之更新，这时候可以用到 useMemo
    // 有没有后面的依赖项数组很重要，否则还是会重新渲染
    // 如果后面的依赖项数组没有值的话，即使父组件的 number 值改变了，子组件也不会去更新
    // const data = useMemo(()=>({number}),[]);
    const data = useMemo(() => ({ number }), [number]);
    console.log('data :>> ', data);
    console.log('data===oldData ',data===oldData);
    oldData = data;

    // 有没有后面的依赖项数组很重要，否则还是会重新渲染
    const addClick = useCallback(()=>{
        setNumber(number+1);
    },[number]);
    console.log('addClick===oldAddClick ',addClick===oldAddClick);
    oldAddClick=addClick;
    return (
        <>
            <input type="text" value={name} onChange={(e)=>setName(e.target.value)}/>
            <SubCounter data={data} onClick={addClick}/>
        </>
    )
}
```


