我们知道echarts的关系图中默认高亮效果是鼠标mouseover和mouseout事件触发的。鼠标移开高亮效果就消失了，但有时候需求需要点击节点后，继续保持高亮效果该怎么办呢。下面分享一下我的解决办法，以供参考。
这是echarts高亮源码：
```JavaScript
el.off('mouseover', el.__focusNodeAdjacency);
el.off('mouseout', el.__unfocusNodeAdjacency);
 
if (itemModel.get('focusNodeAdjacency')) {
    el.on('mouseover', el.__focusNodeAdjacency = function () {
        api.dispatchAction({
            type: 'focusNodeAdjacency',
            seriesId: seriesModel.id,
            dataIndex: el.dataIndex
        });
    });
    el.on('mouseout', el.__unfocusNodeAdjacency = function () {
        api.dispatchAction({
            type: 'unfocusNodeAdjacency',
            seriesId: seriesModel.id
        });
    });
}
```
可以看到监听的是鼠标mouseover和mouseout事件。我们稍作修改，改成监听click事件就好了。
修改后：
```JavaScript
el.off('click', el.__focusNodeAdjacency);
el.off('click', el.__unfocusNodeAdjacency);
if (itemModel.get('focusNodeAdjacency')) {
    el.on('click', function () {
        if (nodeName!= itemModel.option.name) { //判断是否是连续点击同一个节点
            el.__focusNodeAdjacency = api.dispatchAction({
                type: 'focusNodeAdjacency',
                seriesId: seriesModel.id,
                dataIndex: el.dataIndex
            });
            nodeName= itemModel.option.name;
        } else {//如果是连续点击同一个节点，则取消高亮效果
            el.__unfocusNodeAdjacency = api.dispatchAction({
                type: 'unfocusNodeAdjacency',
                seriesId: seriesModel.id
            });
            nodeName= "";
        }
    });
}
```

这个nodeName是我添加的一个全局变量，用来存储点击的节点名称，如果连续点击同一个节点，则取消高亮效果。
![效果图](https://github.com/DimonHo/DH_Note/blob/master/echats/images/image1.gif "效果图")
