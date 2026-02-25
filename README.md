# SetData
SetData是一款在情报分析工作中可以进行数据的交集、差集、并集运算的工具。SetData is a tool for performing intersection, difference, and union operations on data in intelligence analysis.

[Upload# **SetData \- In-Depth User Manual**

**Version**: V1.0 (Local Offline Enhanced Edition)

**Positioning**: A pure front-end, backend-free, lightning-fast data set operator (intersection, union, difference) and regex cleaning tool.

## **📖 Table of Contents**

1. [Software Core Overview]
2. [Global Navigation & Project Management (Top Bar)]
3. [Data Workspace]
4. [Regex Cleaning Engine]
5. [Advanced Data Viewer & Pivot]
6. [Multi-thread Operations Center]
7. [Principles & Performance Limits]

## **1\. Software Core Overview**

SetData is a data processing tool that operates in a closed loop entirely within your web browser. Your data is **never** uploaded to any server, ensuring absolute security and privacy. Its core workflow can be summarized in four simple steps:

**Import Data Sources** ➔ **Regex Cleaning/Formatting** ➔ **Set Logic Operations** ➔ **Multi-dimensional Pivot & Export**.

## **2\. Global Navigation & Project Management (Top Bar)**

The top navigation bar contains core functions that affect the entire workspace.

* **🔍 Global Search**:  
  * **Usage**: Enter a keyword and press Enter.  
  * **Mechanism**: Utilizes Web Worker multi-threading to globally scan all data cards in the workspace, as well as the most recent calculation result.  
  * **Features**: Upon completion, a dedicated viewer pops up, listing hit details in separate Tab pages, and generates a **🕸️ Graph Analysis** (ECharts) to visually display how many times the keyword appears across different data groups.  
* **🕒 Undo (History)**:  
  * **Features**: An extremely detailed time machine. Click the dropdown to view your historical operation stack (e.g., imports, regex extractions, calculations, clears). Every record precisely shows which data group was affected and how many rows were generated.  
  * **Usage**: Click any history record, and the workspace will instantly roll back and completely restore to the state at that exact moment.  
* **🗑️ Clear All**:  
  * Clears all data groups and formulas in the current workspace. An auto-save is triggered before clearing, allowing you to retrieve it via the "Undo" function.  
* **💾 Save Project / 📂 Load Project**:  
  * **Save**: Packages all current workspace data, group names, colors, and even **the entire undo history stack** into a downloadable .json file.  
  * **Load**: Imports a historical .json file to instantly restore your work environment and undo history.  
* **🌐 CN / EN**: One-click seamless switching between Chinese and English interfaces.

## **3\. Data Workspace**

The main central area of the screen, used to manage all data sets (Nodes) participating in operations.

### **3.1 Core Buttons**

* **\[+ Add Group\]**: Manually creates a new empty data set (automatically labeled and color-coded as A, B, C...).  
* **\[Full Screen Icon\]**: Expands the data workspace to full screen, hiding the right-side operations center so you can focus on managing data.

### **3.2 Data Card Details**

Each data set corresponds to a card, containing the following elements:

* **Rainbow Remark Input**: Displays "Enter remark..." by default. It supports multi-level bracket () rainbow highlighting syntax, making it easy to write complex logical tags.  
* **Metadata Stats (Meta)**: The bottom displays the data source (Manual Input / Imported Data / Extract Snapshot / Calculation Result) and **the precise current number of items**.  
* **Card Control Panel (Hover Buttons)**:  
  1. **👁️ View (Full Screen View)**: Opens the "Data Viewer" for deep browsing or traceability.  
  2. **⚡ (Clean & Regex Extract)**: Opens the "Regex Cleaning Engine" to extract targeted data.  
  3. **📁 (Import Data)**: Pops up the local file selector, supporting .xlsx, .xls, .csv, .txt, and .md.  
  4. **🗑️ (Clear Group Data)**: Clears the data within the current card, reverting to the "Manual Input" state while keeping the card itself.  
  5. **❌ (Delete Group)**: Destroys the data group. (Note: Base groups A and B are protected and cannot be destroyed).

### **3.3 Import Data Logic**

After clicking 📁 to import a spreadsheet, the **Import Preview** modal pops up:

1. **Set Starting Row**: Define which row contains the header and which row the data starts from.  
2. **Select Column**: **You must click a column header with your mouse** (the entire column will highlight). SetData uses single-column calculation logic; it extracts one column of key features at a time for set operations.  
3. **Confirm Import**: Once imported, the extracted single-column data will be stored in the corresponding data group.

## **4\. Regex Cleaning Engine**

Click the ⚡ lightning icon on a card to enter this full-screen engine. It uses **non-destructive derivative extraction** logic, ensuring your original data is never altered.

### **4.1 Functional Layout**

* **Left Preset Library**: Built-in professional forensic-level regex libraries (China ID/Phone, International/ID, OSINT/Network, Crypto/Finance, Tech/Hashes). Click any rule to auto-fill the regex pattern.  
* **Custom Library**: After typing your own custom regex, click \[Save Regex\] to store it in the sidebar for future reuse.  
* **Real-time Preview Area**: The bottom black editor loads the source data and highlights (\<mark\>) all segments matched by the regex.  
* **Precision Stats**: The bottom accurately displays Matches (total hits) and Unique (results after deduplication).

### **4.2 Extraction Workflow**

1. Check Global (g) and Insensitive (i) as needed.  
2. Click **\[▶ RUN EXTRACT\]**. The engine completes the extraction and strictly deduplicates the results in the background.  
3. Click **\[Save to Workspace\]** at the bottom. The system will **automatically generate a new data group** (named smartly, e.g., Original Card Name \- \[Regex: China ID\]) and save the extracted results into this new group.  
4. Alternatively, click **\[Export Current View\]** to download directly as Excel/CSV.

## **5\. Advanced Data Viewer & Pivot**

Click the **\[👁️ View\]** button on a card to enter. This is SetData's data observation hub, utilizing Virtual Scroller technology to keep scrolling smooth even with millions of rows.

### **5.1 Viewer Toolbar (Top)**

* **Sort...**: Supports multi-level combination sorting.  
* **Quick Sort (Z-A / A-Z)**: Fast ascending/descending sort on the first column.  
* **Standard Filter...**: Supports multi-condition combination filtering.  
  * *Conditions*: \=, \<\>, \>, \>=, \<, \<=, Contains, Does not contain, Begins with, Ends with, etc.  
  * *Logic*: AND, OR.  
* **Pivot Table...**:  
  * Select **Row Labels** (Group By).  
  * Select **Values** and aggregation methods (Count, Unique Count, Sum, Average, Max, Min).  
  * Upon execution, a new Tab will be generated to display the pivoted results.

### **5.2 Core Mechanism: Global Traceability (Trace)**

When you are viewing a pure text list (like regex extraction results or manually entered data), the viewer automatically scans all data groups in the workspace that were imported as structured tables.

If the data in the current list is found in any structured table, the viewer auto-generates a **\[Trace: Group Name\]** tab, reconstructing the full row context of that data from the original table.

### **5.3 Bottom Functions**

* **Filter Stats**: Displays the remaining number of items after filtering or pivoting in real-time.  
* **Save to Workspace**: Takes a "snapshot" of the currently filtered, sorted, or pivoted data and saves it as a brand-new data group for subsequent calculations.  
* **Export Current View**: Exports the current table state (WYSIWYG).

## **6\. Multi-thread Operations Center**

The right panel is responsible for executing core set logic operations. It uses Web Worker multi-threading, so comparing millions of rows won't freeze the UI.

### **6.1 Set Logic Operations**

Check the boxes in "1. Select Sources" to pick participating groups and designate one as the Base source.

* **\[Intersection \- ∩\]**: Extracts elements that are **commonly shared** among all selected sets.  
* **\[Union \- ∪\]**: Merges data from all selected sets and **strictly deduplicates**.  
* **\[Difference \- \-\]**: Formula is Base Source \- (Union of other sources). Extracts data that exists *only* in the Base source and absolutely not in any other selected source.  
* **\[Symmetric Diff \- Δ\]**: Extracts **non-overlapping** unique elements among the selected sets (i.e., XOR logic, removing the common intersections).

### **6.2 Manual Edit**

Click **\[MANUAL EDIT\]** above the formula screen to expand the keypad:

* Supports typing complex nested logic, such as ( \[A\] ∩ \[B\] ) \- \[C\].  
* Using ( and ) buttons will automatically perform smart text wrapping.  
* Click **\[= RUN\]** to execute multi-threaded calculations.

### **6.3 Result Set Handling**

After calculation, a preview and the result count are displayed below.

* **\[Inspect Context\]**: Enters the Data Viewer, triggering automatic global table tracing to view the contextual environment of these results.  
* **\[Save as New Set\]**: Saves the calculated results as a new node into the workspace (auto-named with the formula) for infinite cascading calculations.  
* **Export**: One-click download of the results as Excel, Txt, or CSV.

## **7\. Principles & Performance Limits**

SetData relies entirely on the browser's V8 engine running purely on the front-end. To ensure the best experience, please understand the following performance boundaries:

* **Optimal Data Volume**: Single file under 10MB, single column data between 100K \~ 300K rows. Within this range, imports, cleaning, and set operations are completed almost instantly with an excellent experience.  
* **Performance Bottlenecks & Lag Zones**:  
  * When single-column data exceeds 500,000 rows, there may be noticeable UI blocking (freezing for a few seconds) during import parsing, regex rendering, or saving, due to the mechanisms of DOM node assignment and full memory deep copying.  
* **Memory Crash Warnings**:  
  * **Strictly avoid** importing .xlsx compressed spreadsheets larger than 50MB. The SheetJS library expands by 3-5 times when decompressing in memory, which can easily cause the browser tab to crash due to Out of Memory (OOM).  
  * If you must process massive data in the tens of megabytes, please **"Save As" a .csv or .txt format first** before importing to bypass the Excel decompression memory wall.  
* **The Cost of History**: The "Undo History" function is extremely detailed. The tradeoff is that every action takes a deep memory snapshot of the entire workspace. If processing million-level data, frequent operations will lead to rapid memory pileup. If you experience lag, it is recommended to save your project, export current results, and refresh the page to clear memory.ing SetData In-Depth User Manual.md…]()



# **SetData (集合数据) \- 深度使用手册**

**版本**: V1.0 (本地离线增强版)

**定位**: 纯前端、无后端的极速数据交并差处理器与正则清洗工具。

## **📖 目录**

1. [软件核心概览]
2. [全局导航与项目管理 (Top Bar)]
3. [数据工作台 (Data Workspace)]
4. [清洗规则引擎 (Regex Cleaning Engine)]
5. [高级数据查看器 (Data Viewer & Pivot)]
6. [多线程运算中心 (Operations)]
7. [原理与性能边界 (Performance Limits)]

## **1\. 软件核心概览**

SetData 是一款在浏览器内闭环运行的数据处理工具，您的所有数据绝不会上传至任何服务器，确保绝对安全。它的核心工作流可以总结为四步：

**导入数据源** ➔ **正则清洗/格式化** ➔ **交并差逻辑运算** ➔ **多维透视与导出**。

## **2\. 全局导航与项目管理 (Top Bar)**

顶部导航栏包含了影响全局的核心功能。

* **🔍 全局搜索 (Global Search)**:  
  * **用法**: 输入关键字后按 Enter。  
  * **机制**: 采用 Web Worker 多线程全局扫描当前工作台中所有卡片的数据以及最近一次运算的结果。  
  * **特色**: 搜索完成后会弹出专属查看器，不仅列出命中明细的 Tab 页，还会生成一个 **🕸️ 关系图谱** (ECharts)，直观展示该关键字在哪些数据组中出现了多少次。  
* **🕒 撤销 (记录) (Undo)**:  
  * **特色**: 极度详尽的时光机。点击下拉可查看历史操作栈（如导入、正则提取、运算、清空等）。每条记录都会精确显示影响了哪个数据组、产生了多少条数据。  
  * **用法**: 点击任意一条历史记录，工作台瞬间回退并完全恢复至该时间点的状态。  
* **🗑️ 一键清空 (Clear All)**:  
  * 清空当前工作台所有数据组和公式。清空前会自动触发一次安全备份，可通过“撤销”找回。  
* **💾 保存项目 / 📂 加载项目**:  
  * **保存**: 将当前工作台的所有数据、分组命名、颜色甚至**全部撤销历史记录**打包为一个 .json 文件下载。  
  * **加载**: 导入历史 .json 文件，瞬间还原工作环境及撤销记录。  
* **🌐 CN / EN (语言切换)**: 一键无缝切换中英文界面。

## **3\. 数据工作台 (Data Workspace)**

屏幕中侧的主区域，用于管理所有参与运算的数据集合（Node）。

### **3.1 核心按钮**

* **\[+ 添加数据组\]**: 手动创建一个新的空数据集（按 A, B, C... 自动标号和分配颜色）。  
* **\[全屏图标\]**: 将数据工作台放大至全屏，屏蔽右侧运算中心以专注管理数据。

### **3.2 数据卡片 (Data Card) 详解**

每个数据集对应一张卡片，包含以下元素：

* **彩虹备注输入框**: 默认显示“输入备注...”。支持多层括号 () 语法的彩虹色高亮，方便编写复杂的逻辑标记。  
* **元数据统计 (Meta)**: 底部显示数据来源（手动输入/已导入/清洗提取/运算结果）以及**当前的精准数据条数 (items)**。  
* **卡片控制面板 (悬浮按钮)**:  
  1. **👁️ View (全屏查看视图)**: 打开“数据查看器”深度浏览或溯源。  
  2. **⚡ (清洗与正则提取)**: 打开“清洗规则引擎”提取靶向数据。  
  3. **📁 (导入数据)**: 弹出本地文件选择器，支持 .xlsx, .xls, .csv, .txt, .md。  
  4. **🗑️ (清空该组数据)**: 清空当前卡片内的数据，退回“手动输入”状态，保留卡片本身。  
  5. **❌ (彻底删除)**: 销毁该数据组。（注：A、B 基础组无法被销毁）。

### **3.3 导入数据逻辑**

点击 📁 导入表格后，会弹出 **数据导入预览** 弹窗：

1. **设置起始行**: 设定表头在哪一行、数据从哪一行开始。  
2. **选择列**: **必须用鼠标点击表头选中某一列**（整列会变色高亮）。SetData 采用单列运算逻辑，一次只能导入一列关键特征进行交并差比对。  
3. **确认导入**: 导入后，提取的单列数据将被存入对应的数据组。

## **4\. 清洗规则引擎 (Regex Cleaning Engine)**

点击卡片上的 ⚡ 闪电图标进入，全屏显示。该引擎采用**非破坏性衍生提取**逻辑，绝不篡改您的原始数据。

### **4.1 功能布局**

* **左侧规则库**: 内置五大类取证级正则库（中国特色、国际/证件、网络侦察、加密货币、取证特征）。点击任意规则，自动填入正则表达式。  
* **自定义库**: 输入自己编写的正则后，点击 \[保存正则表达式\] 即可将其存入侧边栏供以后复用。  
* **实时预览区**: 底部黑色编辑器载入源数据，高亮亮起（\<mark\>）所有被正则表达式命中的部分。  
* **精准统计**: 底部实时显示 匹配个数（总命中数）和 去重个数（Unique 去重后的结果数）。

### **4.2 执行提取工作流**

1. 勾选 Global (g) 全局匹配 和 Insensitive (i) 忽略大小写。  
2. 点击 **\[▶ 执行提取\]**。引擎在后台完成提取并严格去重。  
3. 点击底部的 **\[保存到工作台\]**，系统会**自动生成一个新的数据组**（命名如：原卡片名 \- \[正则: 身份证\]），并将提取结果存入新组。  
4. 或点击 **\[导出当前视图\]** 直接下载为 Excel/CSV。

## **5\. 高级数据查看器 (Data Viewer & Pivot)**

点击卡片上的 **\[👁️ View\]** 按钮进入。这是 SetData 的数据观测枢纽，采用虚拟滚动 (Virtual Scroller) 技术，即使百万行数据也丝滑流畅。

### **5.1 顶部工具栏 (Viewer Toolbar)**

* **排序 (Sort...)**: 支持多级组合排序。  
* **快捷排序 (Z-A / A-Z)**: 对第一列进行极速正序/倒序。  
* **标准筛选 (Filter...)**: 支持多条件组合筛选。  
  * *条件支持*: \=、\<\>、\>、\>=、\<、\<=、包含、不包含、开头是、结尾是等。  
  * *逻辑支持*: AND (与)、OR (或)。  
* **透视汇总 (Pivot Table...)**:  
  * 选择**行标签**（分组依据）。  
  * 选择**计算值**及聚合方式（计数、去重计数、求和、平均值、最大、最小值）。  
  * 执行后会生成一个新的 Tab 页展示透视结果。

### **5.2 核心机制：全网溯源 (Trace)**

当您在查看一个纯文本列表（如正则提取结果或手动输入的数据）时，查看器会自动扫描工作台中所有导入过结构化表格的数据组。

如果发现当前列表中的数据存在于某个结构化表格中，查看器会自动生成 **\[溯源: 数据组名\]** 选项卡，还原该数据在原表格中的整行上下文详情。

### **5.3 底部功能**

* **过滤统计**: 实时显示当前经过筛选或透视后剩余的数据条数。  
* **保存到工作台**: 将当前经过筛选、排序或透视后的数据“快照”，保存为一个全新的数据组参与后续运算。  
* **导出当前视图**: 所见即所得地导出当前的表格状态。

## **6\. 多线程运算中心 (Operations)**

右侧面板，负责执行核心的集合逻辑运算。采用 Web Worker 多线程计算，百万级比对不会卡死 UI 界面。

### **6.1 运算四则逻辑**

在【1. 勾选数据源】中打勾选择参与运算的组，并指定一个 基准 (Base)。

* **\[交集\] (Intersection \- ∩)**: 提取所有选中集合中**共同拥有**的元素。  
* **\[并集\] (Union \- ∪)**: 将所有选中集合的数据合并，并**彻底去重**。  
* **\[差集\] (Difference \- \-)**: 公式为 基准源 \- (其他源的并集)。即提取只存在于基准源中，但绝对不存在于其他选中源中的数据。  
* **\[对称差集\] (Symmetric Diff \- Δ)**: 提取选中集合中**互不重叠**的特有元素（即 XOR 逻辑，去掉公共部分）。

### **6.2 手动编辑公式 (Manual Edit)**

点击公式屏幕上方的 **\[手动编辑\]**，展开键盘：

* 支持输入复杂的嵌套逻辑，如 ( \[A\] ∩ \[B\] ) \- \[C\]。  
* 使用 ( 和 ) 按钮会自动进行智能文本包裹。  
* 点击 **\[= RUN\]** 执行多线程计算。

### **6.3 结果集处理 (Result Set)**

运算完成后，下方会显示预览和结果数量。

* **\[溯源详情\]**: 进入 Data Viewer，自动触发全网表格溯源，查看这些运算结果的上下文环境。  
* **\[结果入库\]**: 将运算结果作为一个新的节点存入工作台（自动带上公式命名），用于下一步的无限级联计算。  
* **导出**: 一键将结果下发为 Excel、Txt 或 CSV。

## **7\. 原理与性能边界 (Performance Limits)**

SetData 依靠浏览器的 V8 引擎纯前端运行。为了获得最佳体验，请了解以下性能边界：

* **最适宜数据量**: 单个文件 10MB 以内，单列数据 10万 \~ 30万行。在此区间内，导入、清洗、交并差运算几乎瞬间完成，体验极佳。  
* **性能瓶颈与卡顿区**:  
  * 单列数据超过 50 万行时，导入解析、正则渲染或保存时，浏览器 UI 可能会有明显的几秒阻塞卡顿（由于 DOM 节点赋值和内存全量深拷贝的机制限制）。  
* **内存崩溃警告**:  
  * **严禁**导入超过 50MB 的 .xlsx 压缩表格。SheetJS 库解压构建时会膨胀 3-5 倍，极易导致浏览器标签页内存溢出 (OOM) 崩溃。  
  * 如果必须处理几十兆的大数据，请将其**另存为 .csv 或 .txt 格式**再导入，以绕过 Excel 解压的内存墙。  
* **历史记录的代价**: “撤销历史”功能极度详尽，代价是每做一步都会对整个工作台进行内存快照深拷贝。如果处理百万级数据，频繁操作会导致内存快速堆积。如感卡顿，可通过导出现有结果并刷新页面释放内存。
