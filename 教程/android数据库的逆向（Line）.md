# android数据库的逆向（Line）

Android数据库：SQLite

但是它不支持加密



所以 apk 在处理的时候有两种加密的方式

1. 写进数据库的数据进行加密
2. 对整个数据库的文件进行加密（通过 SQLiteCipher 这个开源的框架）

---







