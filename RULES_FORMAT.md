# Rules Format 规则格式

## Components.txt / Rules.txt

格式

```
[组件类型]
[应用包名]/[具体组件名]
```

示例

```
service
com.tencent.mm/com.tencent.mm.plugin.appbrand.ipc.AppBrandMainProcessService
com.tencent.mm/com.tencent.mm.booter.CoreService
```

- 组件类型包括 `service` `broadcast` `activity` 
- `Components.txt`文件应包含该应用的所有组件
- `Rules.txt`文件应该包含该应用需要被禁止的组件



## Info.md

规则不固定 主要用于介绍该规则的详细属性 



## [应用包名].xml

格式

```
<rules>
  <[组件类型] block="[true/false]" log="[true/false]" >
    <intent-filter >
      <action name="[具体组件名]" />
    </intent-filter>
  </[component]>
</rules>
```

- 组件类型包括 `service` `broadcast` `activity` 
- `block` 是否开启此组件规则
- `log` 是否开启log
- 该文件内容可通过`Rules.txt`文件内容转换得到
- **转换工具 [ToIFW](https://yamiku.wodemo.com/down/483297/ToIFW.html)**
