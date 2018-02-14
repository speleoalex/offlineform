# offlineform
Add this code within the html page between the <body> tags
<!-- start SaveOfflineForm code -->
    <button type="button" onclick="SaveAs();">Save to Disk</button>
<!-- end SaveOfflineForm code -->



Add this code between the <head> tags :

 <!-- start SaveOfflineForm code -->
        <script>
            (navigator.appVersion.indexOf("MSIE") != -1) && alert("If you use the Explorer browser will not be able to save the data. Use Chrome or Firefox!");
            //Add this code inside the tag "<body>":
            //<button type="button" onclick="SaveAs();">Save</button>
            var DownloadFile = function(data, name) {
                var el = document.createElement('a');
                var ev = document.createEvent("MouseEvents");
                ev.initMouseEvent("click", true, false, self, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
                el.setAttribute("href", 'data:application/octet-stream;base64,' + btoa(unescape(encodeURIComponent(data))));
                el.setAttribute("download", name || self.location.pathname.slice(self.location.pathname.lastIndexOf('/') + 1));
                el.dispatchEvent(ev);
            };
            var SaveAs = function () {
                var elements = document.getElementsByTagName("input");
                for (var i in elements) {
                    try {
                        elements[i].setAttribute("value", elements[i].value);
                        if (elements[i].checked)
                            elements[i].setAttribute("checked", "checked");
                        else
                            elements[i].removeAttribute("checked");
                    } catch (e) {
                    }
                }
                elements = document.getElementsByTagName("textarea");
                for (var i in elements) {
                    try {
                        elements[i].innerHTML = elements[i].value;
                    } catch (e) {
                    }
                }
                elements = document.getElementsByTagName("select");
                for (var i in elements) {
                    if (elements[i].options) {
                        var selectedIndex = elements[i].selectedIndex;
                        for (var o in elements[i].options) {
                            try {
                                elements[i].options[o].removeAttribute("selected");
                            } catch (e) {
                            }
                        }
                        elements[i].options[selectedIndex].setAttribute("selected", "selected");
                    }
                }
                var filename = document.getElementsByTagName("title")[0].innerHTML.replace(/ /g, "_") + "_" +
                        new Date().toISOString().slice(0, 19).replace('T', '_').substr(0, 10) +
                        ".html";
                DownloadFile("<!DOCTYPE html>\n<html>\n" + document.getElementsByTagName("html")[0].innerHTML + "\n</html>", filename);
            }
        </script>
<!-- end SaveOfflineForm code -->
