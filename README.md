# NW_COVID-19_Report
大西北 nCov健康打卡定时自动脚本 [请勿滥用]

基于 Python3 的适用于 XXX 的 COVID-19 自动填报脚本  
现已适配2021年寒假打卡方式
项目用于学习交流，仅用于各项无异常时打卡，如有身体不适等情况还请自行如实打卡

## 使用方式

1. 在企业微信进入“返校打卡”页面，抓包获得'cookies'，修改`id.csv`内的`eai-sess`列(分隔符为`,`)
    ```
    name_id,eai-sess,at_school,custom_area,area
    ```
2. 修改 `report.py` 内的经纬度（可选)  
3. ~~填写 `province` 和 `city`避免报 `上报位置不能为空` 错误；`address`为您的具体地址，如`广东省广州市海珠区阅江西路222号广州塔`；`area`为您所在的行政区域，如`广东省 广州市 海珠区`~~  
4. 如果是留校同学，请修改`id.csv`内的`at_school`列为1，程序将会自动上报位置为`北京市朝阳区北三环东路15号北京化工大学`
5. 如果是离校但需要自定义打卡位置同学，请保持`id.csv`内的`at_school`列为0，并修改`custom_area`列为1，且在`area`列内填写您所在的行政区域，以空格分隔行政级别，如`广东省 广州市 海珠区`，或直辖市`上海市 上海市 静安区`  
6. 如果是离校但只需要~~形式主义一下~~打卡的同学，请保持`id.csv`内的`at_school`列和`custom_area`列为0~~，程序会带您去一个安全的景点旅游XD~~  
7. 安装所需依赖：`pip3 install requests` （Windows下请用命令提示符输入，报错请检查PATH；Linux在shell直接打就行）  

>>`若提示'pip' 不是内部或外部命令，也不是可运行的程序或批处理文件，请加入`PATH`

5. 执行 `ncov_report.py`


### Linux：使用 Crontab

```shell script
sudo crontab -e
```

每天早晨 6 点上报

```shell script
0 6 * * * python3 /home/report/ncov_report.py
```

每两小时上报一次并追加输出到日志

```shell script
0 */2 * * * python3 /home/report/ncov_report.py >> report.log
```
