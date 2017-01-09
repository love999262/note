```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <input type="file" id="fileApi">
    <div id="output"></div>
    <script>
        var filesList = document.getElementById("fileApi");
        function createObjectURL(blob){
            if (window.URL){
                return window.URL.createObjectURL(blob);
            } else if (window.webkitURL){
                return window.webkitURL.createObjectURL(blob);
            } else {
                return null;
            }
        }
        function getFile(){
            var output = document.getElementById("output");
            var files;
            var reader = new FileReader();
            filesList.addEventListener("change",function(event){
                files = event.target.files[0];
                reader.readAsDataURL(files);
                url = createObjectURL(files)
/*                reader.onerror = function(){
                    output.innerHTML = "<img src=\"" + url + "\">";
                }
                reader.onprogress = function(){
                    output.innerHTML = "<img src=\"" + url + "\">";
                }*/
                reader.onload = function(){
                    output.innerHTML = "<img src=\"" + url + "\">";
                }    
            },false);
        }
        window.onload = function(){
            getFile();
        }
    </script>
</body>
</html>
```
其中window.URL.createObjectURL(blob)指向当前file的url地址，参数blob表示二进制.
