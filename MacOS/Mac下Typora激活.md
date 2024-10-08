### Mac下Typora激活

##### 操作

1. vim编辑/Applications/Typora.app/Contents/Resources/TypeMark/page-dist/static/js/Licen..文件
2. 查到hasActivated="true"==e.hasActivated修改为hasActivated="true"=="true"

3. resources\page-dist\\license.html

4. 查到`</body></html>`

   替换为

   `</body><script>window.onload=function(){setTimeout(()=>{window.close();},5);}</script></html>`

5. 编辑/Applications/Typora.app/Contents/Resources/TypeMark/locales/zh-Hans.lproj
6. "UNREGISTERED":"未激活"替换为"UNREGISTERED":" ",
