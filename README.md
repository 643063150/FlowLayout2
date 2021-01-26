# FlowLayout2
基于https://github.com/yangsanning/FlowLayout2 修改，增加了行数限制

## 效果预览

| FlowLayout2                      |
| ------------------------------- |
| <img src="images/image1.gif" height="512" /> |


## 主要文件
| 名字             | 摘要           |
| ---------------- | -------------- |
|FlowLayout2 | 流布局  |
|BaseFlowLayout2Adapter | adapter(核心)  |
|BaseFlowLayout2ViewHolder | ViewHolder  |
|BaseFlowLayout2Type | 多类型布局  |

### 1. 基本用法

#### 1.1 布局中添加
```android
<ysn.com.view.flowlayout2.FlowLayout2 
    android:layout_width="match_parent"
    android:layout_height="match_parent"  
    ysn:fl2_column_space="10dp"
    ysn:fl2_row_space="10dp" />
```

#### 1.2 简单示例
```android
    FlowLayout2Adapter flowLayout2Adapter = new FlowLayout2Adapter();
    flowLayout2.setAdapter(flowLayout2Adapter);
    flowLayout2Adapter.setNewData(getData());
    
    private class FlowLayout2Adapter extends BaseFlowLayout2Adapter<User, BaseFlowLayout2ViewHolder> {

        protected FlowLayout2Adapter() {
            super(R.layout.item_flow_layout_2);
        }

        @Override
        public void convert(BaseFlowLayout2ViewHolder holder, int position, User item) {
            holder.setText(R.id.flow_layout_2_item_text, item.getName());
        }
    }
```

#### 1.2.1 点击事件配置(可选)
```android
    flowLayout2Adapter.setOnItemClickListener(onItemClickListener)
    flowLayout2Adapter.setOnItemLongClickListener(onItemLongClickListener)
    holder.setOnClickListener(onClickListener)
    holder.setOnLongClickListener(onLongClickListener)
```

#### 1.2.2 空布局的配置(可选)
```android
    // 设置空布局
    flowLayout2Adapter.setEmptyLayoutRes(R.layout.layout_empty);
    
    // 可通过getEmptyView获取空布局, 进行相关操作
    flowLayout2Adapter.getEmptyView().setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            flowLayout2Adapter.setNewData(getData());
        }
    });
```

#### 1.2.2 多布局的配置(可选)
```android
    // 注意: 一定要先设置FlowLayout2Type, 方可进行相关操作
    setFlowLayout2Type(new BaseFlowLayout2Type<User>() {
        @Override
        protected int getItemType(User user) {
            return user.getId() % 2 == 1 ? 0 : 1;
        }
    });

    // 可通过获取FlowLayout2Type进行类型绑定
    getFlowLayout2Type().addItemType(0, R.layout.item_multi_type_flow_layout_2_1);

    // 可直接进行类型绑定
    addItemType(1, R.layout.item_multi_type_flow_layout_2_2);
```


### 2. 配置属性

#### FlowLayout2
|name|format|description|
|:---:|:---:|:---:|
| fl2_column_space | dimension | 列的间距 |
| fl2_row_space | dimension | 行的间距 |
| fl2_is_last_avg | boolean | 最后一行是否均分 |
| maxLines | integer | 行数，0不限制行数 |
