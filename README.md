* 创建新文章(hello指文章名称)
```
hexo new hello
```
* 部署
```
hexo deploy
```
* 启动本地服务
```
hexo server
```
* 使用 Hexo 生成静态文件
```
hexo generate
```
* Hexo 能够监视文件变动并立即重新生成静态文件，在生成时会比对文件的 SHA1 checksum，只有变动的文件才会写入。
```
hexo generate --watch
```
* Hexo 在生成完毕后自动部署网站
```
hexo generate --deploy
```