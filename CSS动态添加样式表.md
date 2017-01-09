```
var styleSheet= {
    addStyleSheet: function(url) {
        var link = document.createElement("link");
        link.setAttribute("rel", "stylesheet");
        link.setAttribute("type", "text/css");
        link.setAttribute("href", url);
        var heads = document.getElementsByTagName("head");
        document.documentElement.appendChild(link);
    },
    removeStyleSheet: function(url) {
        var links = document.getElementsByTagName("link")
        for (var i = 0; i < links.length; i++) {
            if (links[i].href = url) {
                links[i].parentNode.removeChild(links[i]);
            } else {
                return;
            }
        }
    }
}

```
