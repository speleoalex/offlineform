# offlineform
Add this code within the html page between the <body> tags
<!-- start SaveOfflineForm code -->
    <button type="button" onclick="SaveAs();">Save to Disk</button>
<!-- end SaveOfflineForm code -->



Add this code between the <head> tags :

<!-- start SaveOfflineForm code -->
<script>
            -1!=navigator.appVersion.indexOf("MSIE")&&alert("If you use the Explorer browser will not be able to save the data. Use Chrome or Firefox!");var DownloadFile=function(e,t){var a=document.createElement("a"),n=document.createEvent("MouseEvents");n.initMouseEvent("click",!0,!1,self,0,0,0,0,0,!1,!1,!1,!1,0,null),a.setAttribute("href","data:application/octet-stream;base64,"+btoa(unescape(encodeURIComponent(e)))),a.setAttribute("download",t||self.location.pathname.slice(self.location.pathname.lastIndexOf("/")+1)),a.dispatchEvent(n)},SaveAs=function(){var e=document.getElementsByTagName("input");for(var t in e)try{e[t].setAttribute("value",e[t].value),e[t].checked?e[t].setAttribute("checked","checked"):e[t].removeAttribute("checked")}catch(e){}for(var t in e=document.getElementsByTagName("textarea"))try{e[t].innerHTML=e[t].value}catch(e){}for(var t in e=document.getElementsByTagName("select"))if(e[t].options){var a=e[t].selectedIndex;for(var n in e[t].options)try{e[t].options[n].removeAttribute("selected")}catch(e){}e[t].options[a].setAttribute("selected","selected")}var o=document.getElementsByTagName("title")[0].innerHTML.replace(/ /g,"_")+"_"+(new Date).toISOString().slice(0,19).replace("T","_").substr(0,10)+".html";DownloadFile("<!DOCTYPE html>\n<html>\n"+document.getElementsByTagName("html")[0].innerHTML+"\n</html>",o)};
</script>
<!-- end SaveOfflineForm code -->

