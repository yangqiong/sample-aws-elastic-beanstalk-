## AWS Elastic Beanstalk 部署 nextjs

1. 在 Elatic Beanstalk 中添加环境变量`NPM_USE_PRODUCTION`为`false`

- 原因: 默认不安装 devDependencies，发现 npm run build 过程中 tailwind 报错
- 参考[Configuring your application's dependencies](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/nodejs-platform-dependencies.html)

2. 在 `predeploy`步骤中执行`npm run build`

- 原因: 由于`npm run start`启动前需要执行`npm run build`，但是比较耗时，所以提前执行
- 参考[AWS Eastic Beanstalk 执行过程](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/platforms-linux-extend.html)

3. start 命令调整为 `npm rebuild && next start -p 8080`

- 原因 1: 项目发布会从 staing 重命名到 current，启动报错，需要重建 node_modules
- 原因 2: Elastic Beanstalk 默认服务关联端口 8080
