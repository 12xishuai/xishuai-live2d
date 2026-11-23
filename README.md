# xishuai-live2d

Live2D 看板娘脚本，基于 Sky 的版本自用托管。

基于 [live2d_demo / ©fghrsh / GPL v2.0](https://github.com/fghrsh/live2d_demo) 修改，原始脚本由 Sky 定制封装为单文件版本。本仓库仅用于通过 jsDelivr 自托管 `kbn.js`，供个人在移动端浏览器（如 Via）使用。

## 文件说明

- `kbn.js`：封装了 Live2D 资源与库文件的单文件脚本

## 使用方式

在网页 HTML 中先配置参数，再动态插入脚本（移动数据与 WiFi 下均可加载）：

```html
<!-- 看板娘：配置前置 + 动态插入 -->
<script>
(function () {
  var w = window;

  // 配置（必须在 kbn.js 执行前定义）
  w.kbn_setting0 = 6;          // 人物 ID
  w.kbn_setting1 = 19;         // 衣服 ID
  w.kbn_setting2 = true;       // 允许关闭（false 则不显示关闭按钮）
  w.kbn_setting3 = '180x170';  // 看板娘尺寸
  w.kbn_setting4 = 'right:10'; // 停靠侧
  w.kbn_setting5 = '160x50';   // 提示框尺寸
  w.kbn_setting6 = '14px';     // 提示框字号
  w.kbn_setting7 = '-13px';    // 工具栏 Y 偏移
  w.kbn_setting8 = '18px';     // 工具栏图标大小
  w.kbn_setting9 = '36px';     // 工具栏行高
  w.kbn_setting10 = null;      // 一言 API，null 用默认 jinrishici.com

  // 防重复执行（不判断网络类型，任何网络都加载）
  var key = encodeURIComponent('看板娘:执行判断');
  if (w[key]) return;

  try {
    w[key] = true;
    var lib = document.createElement('script');
    // 注意：这里请替换为你自己的 jsDelivr 链接
    lib.src = 'https://cdn.jsdelivr.net/gh/12xishuai/xishuai-live2d@1.0.0/kbn.js';
    lib.defer = true;
    document.body.appendChild(lib);
  } catch (err) {
    console.log('看板娘：', err);
  }
})();
</script>
​```

## 配置参数说明

| 变量 | 含义 | 默认值 |
| :--- | :--- | :--- |
| `kbn_setting0` | 人物 ID | `6` |
| `kbn_setting1` | 衣服 ID | `19` |
| `kbn_setting2` | 允许关闭（是否显示关闭按钮） | `true` |
| `kbn_setting3` | 看板娘尺寸 | `'180x170'` |
| `kbn_setting4` | 停靠侧与距离 | `'right:10'` |
| `kbn_setting5` | 提示框尺寸 | `'160x50'` |
| `kbn_setting6` | 提示框字体大小 | `'14px'` |
| `kbn_setting7` | 工具栏 Y 轴偏移 | `'-13px'` |
| `kbn_setting8` | 工具栏图标大小 | `'18px'` |
| `kbn_setting9` | 工具栏行高 | `'36px'` |
| `kbn_setting10` | 一言 API | `null`（默认 jinrishici.com） |

## jsDelivr 引用格式

​```text
https://cdn.jsdelivr.net/gh/12xishuai/xishuai-live2d@版本号/kbn.js
​```

例如版本号为 `1.0.0` 时：

​```text
https://cdn.jsdelivr.net/gh/12xishuai/xishuai-live2d@1.0.0/kbn.js
​```

配置好后，看板娘就能在 Via 首页中陪伴您了。

## 可能存在的 BUG

- 点击"关闭看板娘"按钮后，可能会导致**浏览器卡死**！暂时未探明原因。若遇到该问题，建议通过设置 `w.kbn_setting2 = false` 来隐藏关闭按钮，从而规避此问题。
- 部分分辨率较低设备可能会出现发言气泡显示内容不全的问题，若出现此问题可以修改脚本开头的 `w.kbn_setting5` 参数，把气泡改大。

## 免责声明

- 此插件仅适用于个人技术研究学习，请勿商用。
- 出现任何法律纠纷，与作者无关。
