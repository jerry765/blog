title: high performance javascript
date: 2023-11-13 15:04:11
mdate: 2023-11-13 15:21:02
doc_id: a6c6a56af06247d9b0f520d8c092cd71

优化`JavaScript`规则：
1. 将脚本放在底部：脚本阻塞资源下载
2. 减少外链脚本文件（合并）
3. 无阻塞脚本（页面加载完成后加载脚本 `defer`）

动态加载`Javascript`文件
``` js
function loadScript(url, callback) {
    let script = document.createElement(“script”)
    script.type = “text/javascript”

    if (script.readyState) {  // IE
        script.onreadystatechange = function(){
            if (script.readyState == “load” || script.readyState == “complete”) {
                script.onreadyState = null
                callback()
            }
        }
    } else {
        script.onload = function() {  // other browsers
            callback()
        }    
    }

    script.scr = url
    document.head.appendChild(script)
}

// example
loadScript(“file1.js”, function(){
    alert(“File is loaded!”)
})
```

