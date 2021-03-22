### 搭建 vue 项目

---

##### 一、安装 node 环境

1. 下载地址为： https://nodejs.org/en/
2. 检查是否安装成功：如果输出版本号，说明 node 环境安装成功
   ![Image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue01.png)
3. 设置 nodejs prefix(全局)和 cache(缓存)路径

```
在nodejs安装路径下，新建node_global 和 node_cache两个文件夹
```

![Image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue04.png)

- 设置缓存文件夹

```
npm config set cache "c:\ruanjian\nodejs\node_cache"
```

- 设置全局模块存放路径

```
npm config set prefix "c:\ruanjian\nodejs\node_global"
```

> 设置成功后，之后用命令 npm install XXX -g 安装以后模块就在 c:\ruanjian\nodejs\node_golbal 4. 安装淘宝 cnpm 命令管理工具替代默认的 npm 管理工具(因为国内使用 npm 非常慢，推荐使用淘宝 npm 镜像)

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue02.png)

- 验证是否安装成功

```
cnpm -v
```

- 安装成功如下图
  ![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue03.png)

5. 设置环境变量(非常重要)
   > 设置环境变量可以使得在热议目录下都可以使用 cnpm、vue 等命令，而不需要输入全路径

- 右键"此电脑"，选择 属性-系统-高级系统设置-系统属性,修改系统变量 PATH
  ![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue05.png)
  ![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue06.png)
  ![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue07.png)
- 新增系统变量 NODE_PATH
  ![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue08.png)

6. 安装 vue 命令行工具，即 vue-cli 脚手架

```
npm install vue-cli -g
或
cnpm install -g vue-cli
```

![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue11.png)

- 卸载 vue-cli

```
npm uninstall vue-cli -g
```

![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue12.png)

- vue-cli 版本查看

```
vue -V
```

![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue10.png) 7. 用 vue-cli 构建项目

```
vue init webpack my_project
```

![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue13.png) 8. 安装依赖

```
1）输入：cd my_project (项目名)，回车，进入到具体项目文件夹
2）输入：cnpm install，回车，等待一会
回到项目文件夹，会发现项目结构多了一个node_modules文件夹(该文件夹的内容就是之前安装的依赖)
```

![image](https://raw.githubusercontent.com/luzeping966/knowledgeBase/master/images/vue14.png) 9. 测试环境是否搭建成功

```
1）在cmd里输入：npm run dev
2）在浏览器里输入：http://localhost:8080（默认端口8080）
```
