# VCB-S-generate-pubfile
生成 VCB-S 发布文件 bangumi.html, vcbs.html  

## 功能
将说明性内容写入同文件夹对应 txt 文件中，程序读取文件，生成并写入最终的发布文件。  
- process_chn/eng.txt 画质吐槽 中 / 英
- rs_chn/eng.txt 重发修正 中 / 英
- screenshot.txt 对比截图链接
- mediainfo.txt
- link.txt 发布链接

## 使用
- 每次打开程序时，会载入 content/doc.xml（在每次点击生成按钮时更新并保存），恢复上次生成时保存的内容。
- 所有输入框可以右键双击以清除内容。
- 所有按钮对应的 txt 文档都保存在 content/ 文件夹中，若不存在则点击按钮时自动创建。
  - 程序会自动处理 txt 的最后一行为回车换行，若有则保留，若没有则自动添加。但无法自动删除多个多余空白行。
1. 发布图-bt：填写上传至 [VCB-S 萌图床](https://img.2222.moe/vcbs) 的 _800 竖图 url。
2. 发布图-vcbs：仅当 _1400 横图需要声明 Image Credit 时，输入原图 pixiv 链接。
   - 将会自动获取作者，在 vcbs.html 生成 Image Credit。
3. 当有合作字幕组时，点击“添加字幕组”按钮，在列表中选择字幕组中文名即可。
   - 如需修改字幕组信息，则修改 util/data.py 中的 SUB 字典。
   - 程序会根据 SUB 字典自动匹配字幕组英文名，根据发布文档在对应的地方使用。
   - 当前最多支持 3 个字幕组。添加更多字幕组时，下拉菜单会移除已经选过的字幕组。
   - 当前暂不支持移除字幕组，并且若不选择字幕组会提示 bug。
   - 当前暂不支持从 xml 文件恢复字幕组。
4. 标题区：对应输入中/英/日文标题。
   - 英文标题长度大于 30 时，判定为长标题：
     - 分行显示标题，bt 发布标题不添加日文，并添加长路径警告。
     - 如需修改长标题阈值，则修改 util/data.py 中的 THTITLE。
   - 中文标题的第一组有效字符作为发布文件名（比如：中文标题“电锯人 / 链锯人”，则文件名为“电锯人”）。
5. 规格区：分别对应 规格、类型、内容、标记：
   - 规格 10-bit 1080p HEVC，一般不需要修改。
   - 类型 DVDRip / WebRip / TVRip (格式自由)，一般不需要修改。
   - 内容 TV S1 / Movie / TV S2 + OVA (格式自由)
   - 标记 Reseed / Rev
6. 复选框-重发：选中时在标记处添加 Reseed，并生成修正区：
   - 重发修正-中/英文：按钮分别打开对应的 txt 文档，在其中输入对应的信息。
7. 其他复选框：选中则添加对应的中英陈述。
   - 内封原盘 ENG + JPN 字幕。
   - 内封评论音轨。
   - 部分剧集内封评论音轨。
   - 外挂 FLAC 5.1 + Headphone X。
   - 当前内容直接复制发布规范，需根据实际情况自行修改。
8. 画质 小作文-中/英文：按钮分别打开对应的 txt 文档，在其中输入对应的信息。
9. 感谢：输入来源感谢信息，建议直接从 trello 或 r21 复制。
10. 吐槽：输入发布吐槽，没有则留空。
11. 对比截图：按钮打开对应的 txt 文档，在其中输入 url 中 html 格式的对比图。
12. mediainfo：按钮打开对应的 txt 文档，在其中输入对应的信息。
    - 可以自动将 mediainfo 中的文件路径替换为 D:\SAYA IS ∞ LOLICON!
      - 需根据实际文件路径修改 util/data.py 中 MYFOLDER 的值
13. 发布链接区：可以手动输入发布链接以生成发布文件。但有更便捷的方案。
14. 编辑发布链接：按钮打开对应的 txt 文档，在其中输入：
    - 第 1 行复制 bangumi 发布链接。
    - 2-5 行复制 bangumi 提供的团队同步内容。
      - 直接多行复制即可，无需逐个复制链接，程序会自动删掉前缀部分，中英前缀皆可。
    - 第 6 行复制 nyaa 发布链接。
15. 更新发布链接：按钮会更新 link.txt 中的链接：
    - 发布链接只保留 url 部分。
    - 在下方生成 vcbs 发布用的 6 行 a 标签。
    - 同时更新界面中的链接区。
16. 生成：按钮会在当前文件夹生成 2 个发布文件 中文标题-bangumi/vcbs.html。
    - 点击生成按钮时，如果成功则程序自动退出。
    - 点击生成按钮时，会更新并保存 content/doc.xml，下次打开程序时恢复上次保存的内容。

## 更新
- v3.6
  - 修改长标题阈值 25 -> 30
  - 规范注释，添加更详细的使用说明
  - 为 img_1400 添加爬虫功能，输入 pixiv 链接可自动获取作者并添加 image credit
  - 优化 mediainfo，自动替换文件路径
- v3.5
  - 添加纵向滚动条
  - 行布局从固定数字改为 row_curr 变量，便于修改布局
  - 界面优化，按钮改为更直观的中文，更新发布链接时可支持中文 bangumi 团队同步
- v3.4
  - 引入 xml 保存上次编辑
  - 取消输入框焦点清空功能，改为右键双击触发
  - 修正中文名含有特殊字符时无法作为文件名的问题
  - 取消 img_1400 相关功能
- v2.6
  - 整理程序结构，在 util 文件夹中以 data.py 存储数据，func.py 存储函数
  - 调整界面设计，修改变量名称
  - 将字幕组输入改为选项模式
  - 更改文件类型为 pyw，并打包 exe 发布
  - 更新发布链接编辑与生成方式，添加编辑和更新按钮。
  - 修正并优化输入框焦点清空问题
  - 智能修正 txt 末行空格、空行问题
- v1.2
  - 改用外置 txt 文件编辑、存取相应文本信息
  - 整理文件结构，文本信息放入单独文件夹 info
- v0.3
  - 基本界面设计，功能验证
  - 生成发布文件-bt
  - 生成发布文件-主站
