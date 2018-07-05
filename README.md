# CodeMirror手册

## 下载：

CodeMirror的官网是：[CodeMirro](http://codemirror.net/)

代码托管在Github上，下载地址：[github](https://github.com/codemirror/CodeMirror/archive/master.zip)

## 引入：

```$xslt
<!-- 引入CodeMirror核心文件 -->
<script type="text/javascript" src="codemirror/lib/codemirror.js"></script>

<!-- CodeMirror支持不同语言，根据需要引入JS文件 -->
<!-- 因为HTML混合语言依赖Javascript、XML、CSS语言支持，所以都要引入 -->
<script type="text/javascript" src="codemirror/mode/javascript/javascript.js"></script>
<script type="text/javascript" src="codemirror/mode/xml/xml.js"></script>
<script type="text/javascript" src="codemirror/mode/css/css.js"></script>
<script type="text/javascript" src="codemirror/mode/htmlmixed/htmlmixed.js"></script>

<!-- 下面分别为显示行数、括号匹配和全屏插件 -->
<script type="text/javascript" src="codemirror/addon/selection/active-line.js"></script>
<script type="text/javascript" src="codemirror/addon/edit/matchbrackets.js"></script>
<script type="text/javascript" src="codemirror/addon/display/fullscreen.js"></script>
```

## html代码：

```html
 <div class="wrap">
     <div class="header">
         <h1>Qianwei</h1>
     </div>
     <div class="content">
         <div class="input">
             <div class="input_title">
                 <input type="button" value="源代码">
                 <input type="button" value="运行" id="run">
             </div>
             <div class="input_area">
                 <textarea id="code" name="code"></textarea>
             </div>
         </div>
         <div class="input">
             <div class="input_title">
                 <input type="button" value="运行结果">
             </div>
             <div class="input_area" id="result">
 
             </div>
         </div>
     </div>
 </div>
```

## CSS代码：
```css
<style>
        * {
            margin: 0;
            padding: 0
        }

        .wrap {
            width: 100%;
            height: 100%;
        }

        .header {
            width: 100%;
            height: 60px;
            background: #96b97d;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }

        .content {
            margin-top: 40px;
            display: flex;
            justify-content: space-around;
            padding: 0 20px;
        }

        .input {
            width: 650px;
            height: 500px;
            border: 1px solid #ddd;
            box-shadow: 0 1px 1px rgba(0, 0, 0, .05);
        }

        .input_title {
            width: 650px;
            height: 60px;
            background-color: #f5f5f5;
            border-bottom: 1px solid #ddd;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 20px;
            box-sizing: border-box;
        }

        input[type='button'] {
            border: 1px solid #ddd;
            outline: none;
            width: 85px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            color: #333333;
            border-radius: 5px;
            background: #fff;
        }

        .input_area {
            width: 650px;
            height: calc(500px - 60px);
            box-sizing: border-box;
        }

        textarea {
            width: 650px;
            height: calc(500px - 60px);
            border: none;
            outline: none;
            resize: none;
        }


        iframe {
            width: 650px;
            height: calc(500px - 60px);
            border: none;
            outline: none;
        }
        .CodeMirror {
            position: relative;
            overflow: hidden;
            background: white;
            width: 100%;
            height: 100%;

        }
    </style>
```

## Js代码：
```javascript
<script>
    var editor = CodeMirror.fromTextArea(document.getElementById("code"), {
            lineNumbers: true,     // 显示行数
            indentUnit: 4,         // 缩进单位为4
            styleActiveLine: true, // 当前行背景高亮
            matchBrackets: true,   // 括号匹配
            mode: 'htmlmixed',     // HMTL混合模式
            lineWrapping: true    // 自动换行
        });
    
        var Run = document.querySelector("#run");
    
        var Result = document.querySelector("#result");
    
    
    
        Run.onclick = function () {
            Result.innerHTML = "";
            var htmlCode = editor.getValue();
            // 1. 创建<iframe>元素
            var iframe = document.createElement('iframe');
            // 2. 将CSS，HTML字符串转换为Blob对象
            var blob = new Blob([htmlCode], {
                'type': 'text/html'
            });
            // 3. 使用URL.createObjectURL()方法将...
            iframe.src = URL.createObjectURL(blob);
    
            Result.appendChild(iframe)
        }
</script>
```










