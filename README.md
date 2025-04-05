

Core framework: Vue2.x, Vue Router, Vuex

Vue project is built based on @vue/cli4.x

JS dependencies and referenced CSS: [axios](https://github.com/axios/axios) , [moment](https://github.com/moment/moment) , [nprogress](https://github.com/rstacruz/nprogress) , [v-viewer](https://github.com/fengyuanchen/viewerjs) , [prismjs](https://github.com/PrismJS/prism) , [APlayer](https://github.com/DIYgod/APlayer) , [MetingJS](https://github.com/metowolf/MetingJS) , [lodash](https://github.com/lodash/lodash) , [mavonEditor](https://github.com/hinesboy/mavonEditor) , [echarts](https://github.com/apache/echarts) , [tocbot](https://github.com/tscanlin/tocbot) , [iCSS](https://github.com/chokcoco/iCSS)

### Backstage UI

Backend CMS is partly based on [vue-admin-template](https://github.com/PanJiaChen/vue-admin-template)

The UI framework is [Element UI](https://github.com/ElemeFE/element)

### Front-end UI

[Element UI](https://github.com/ElemeFE/element) : Partial use, some small components, changed the UI style to facilitate quick effect

## Recently Updated

Add label function

Improve some UI

Docker front-end deployment method

Docker Compose one-click deployment

# Quick Start

Docker deployment method (recommended, can be used for rapid launch or testing)

```
# 未安装docker的请先安装docker，已经安装的跳过此步
yum install docker-ce -y
#启动docker
systemctl start docker
# 配置国内源
# 创建docker目录
sudo mkdir -p /etc/docker
# 创建配置文件
sudo tee /etc/docker/daemon.json <<-'EOF'
{
"registry-mirrors": ["https://mirror.ccs.tencentyun.com"]
}
EOF
# 加载新的配置文件
sudo systemctl daemon-reload
# 重启docker服务
sudo systemctl restart docker

main-命令执行
Ps:按顺序执行

1.运行Mysql容器
docker run -d -p 0:3389 \
--name ice-sql \
--restart always \
thecosy/icemysql:v2.2.0

2.运行Spring容器
docker run -d -p 8181:8181 \
--name ice-api \
--restart always \
--link ice-sql:db \
thecosy/icecms:v2.2.0

3.运行Vue容器
docker run -d -p 3000:80 \
--name ice-vue \
--restart always \
--link  ice-api:iceApi \
thecosy/icevue:v2.2.0

#访问前端地址http://ip:3000
```

## Directory Structure

```
iceCMS/
├── HELP.md
├── IceCMS-java.iml
├── IceCMS-main             --java主程序启动入口
│   ├── IceCMS-main.iml
│   ├── main.iml
│   ├── pom.xml
│   ├── src
│   └── target
├── IcePay-ment             --java支付模块
│   ├── IcePay-ment.iml
│   ├── pom.xml
│   ├── src
│   └── target
├── IceWk-ment              --java前端api模块
│   ├── IceWk-ment.iml
│   ├── pom.xml
│   ├── src
│   └── target
├── IceWk-uniApp            --h5Uniapp模块
│   ├── App.vue
│   ├── LICENSE
│   ├── components
│   ├── main.js
│   ├── manifest.json
│   ├── nPro
│   ├── package-lock.json
│   ├── package.json
│   ├── pages
│   ├── pages.json
│   ├── static
│   ├── store
│   ├── subPage
│   ├── template.h5.html
│   ├── theme
│   ├── uni.scss
│   ├── uni_modules
│   ├── utils
│   └── vue.config.js
├── IceWk-vues                --前端vue模块
│   ├── LICENSE
│   ├── README.md
│   ├── babel.config.js
│   ├── build
│   ├── dist
│   ├── jest.config.js
│   ├── jsconfig.json
│   ├── node_modules
│   ├── package-lock.json
│   ├── package.json
│   ├── postcss.config.js
│   ├── public
│   ├── serverless.yml
│   ├── src
│   ├── vue.config.js
│   └── yarn.lock
├── README.md
├── bin
│   ├── clean.bat
│   ├── package.bat
│   └── run.bat
├── doc
│   └── IceCMS环境使用手册.docx
├── mvnw
├── mvnw.cmd
├── pom.xml
└── sql                        --项目sql文件
├── icecms5.6.sql
└── icecms8.0.sql
```

## <strong>Configuring a minimal development environment</strong>

1. Environment Configuration

MySQL JDK1.8 or above Maven Nodejs WeChat Developer Tools

### <strong>Backend deployment</strong>

2. Create the MySQL database `IceCMS` and execute `/sql/IceCMS.sql` to initialize the table data

3. Start the backend service of iceCMS-main management background

3.1. Modify the configuration information `IceCMS-main/src/main/resources/application.yml` to configure the database connection

3.2. Install Redis and start it (it will not affect you if you don't use it)

3.3. Open the command line and enter the following command

```
cd iceCMS
mvn install
mvn clean package
java -Dfile.encoding=UTF-8 -jar iceCMS/iceCMS-main/target/iceCMS.jar
#在iceCMS.jar目录输入 java -jar iceCMS.jar
```

### <strong>Front-end deployment</strong>

4. Enter the iceCMS-vues directory

Open the command line and enter the following command

```bash
# 克隆项目
git clone https://github.com/PanJiaChen/vue-admin-template.git

# 进入项目目录
cd IceWk-VUE

# 安装依赖
npm install

# 建议不要直接使用 cnpm 安装以来，会有各种诡异的 bug。可以通过如下操作解决 npm 下载速度慢的问题
npm install --legacy-peer-deps --registry=https://registry.npm.taobao.org
# 启动服务
npm run dev
```

### release

```bash
# 构建测试环境
npm run build:stage

# 构建生产环境
npm run build:prod
```

5. Start the front end

Open the browser and visit [http://localhost:9528](http://localhost:9528) to enter the front-end page.

Start the front-end backend (backend address http://localhost:9528/admin)

6. Start the uniapp mobile terminal

Download HBuilderX

Enter the uniapp mobile plug-in directory ( [https://ext.dcloud.net.cn/plugin?id=9261](https://ext.dcloud.net.cn/plugin?id=9261) ), click Import, and then import it to the local computer.

You can also open the IceCMS-uniapp project locally

Open the `IceWK-uniApp` directory and compile and package it

## Precautions

Some common questions:

- MySQL usually has no problem ensuring that the database character set is `utf8mb4` (many table fields such as "Site Settings" and "Article Details" require the `utf8mb4` character set to support emoji emoticons. Otherwise, when importing the sql file, even if the import is successful, some field contents will be incomplete, resulting in an error when rendering data on the front-end page)
- Make sure Maven can successfully import the current version of the dependency. Do not upgrade or downgrade the dependency version.
- The default username and password in the database are `root` and `123123` Because it is a personal project, I don't plan to make a password modification page. You can manually generate a password and store it in the database in the `main` method under `top.naccl.util.HashUtils`
- Note: modify the configuration information of `application-dev.properties` in the IceCMS-main directory
    - If Redis has no password, leave it blank
    - Be careful to modify `token.secretKey` , otherwise the security of token cannot be guaranteed.

## Commercial Use

- If you want to use this project for commercial purposes, I hope you can strictly follow the GPL-3.0 agreement;
- If you really need closed-source commercial use and cannot execute the GPL-3.0 agreement, you can choose:
- Becoming a contributor to a project generally includes:
- Your code is referenced as a dependency by this project;
- The PR you submitted is merged into this project (only valuable ones, excluding simple typos or spelling errors, etc.);
- You have participated in the design and implementation of this project (including providing valuable ideas for the implementation of various functions/modules or the repair of bugs);
- Contact the author for commercial use

## Thanks

Thanks to [JetBrains](https://www.jetbrains.com/) for providing the non-commercial open source software license

## Star History

[](https://star-history.com/#Thecosy/IceCMS&Date)![Star History Chart](https://api.star-history.com/svg?repos=Thecosy/IceCMS&type=Date)



