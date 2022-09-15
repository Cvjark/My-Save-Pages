
- [x] Ctags 的安装，这个的安装比较简单，设置也是，属于VScode必装插件
- [x] [（部分）解决--c/c++环境出现“检测到 #include 错误，请更新 includepath。”](。。。) 最终解决方案请看下一条
- [ ] [IntelliSenseMode 已更改，因为它与检测到的编译器不匹配。请考虑改为设置 \"compilerPath\"。将 \"compilerPath\" 设为 \"\" 以禁用系统包含和定义的检测。"](...)
  查找网上的解决方案是修改 VScode 下的 c_cpp_properties.json 文件。笔者机器上的该文件如下：
  ```
  {
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "cStandard": "c17",
            "cppStandard": "c++17",
            "intelliSenseMode": "windows-msvc-x64"  // 修改为 "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
  }
  ```
  提交上述修改，重启 VScode 之后依旧存在错误，随后仔细查看错误提示：
  
  `\"compilerPath\"。将 \"compilerPath\" 设为 \"\" 以禁用系统包含和定义的检测` 
  随后在 VScode -> setting 中找到 compilerPath，配置为 MinGW 的 gcc.exe ，如下图：
 
  ![image](https://user-images.githubusercontent.com/89090949/190464216-38ef8f07-4d81-444b-b87d-55531fa51e0c.png)
 
  随后问题解决

