# 1. 源站的配置 （很重要）
源站需要配置成一个简单的返回200状态码的页面，且不对请求进行任何过滤和拦截，否则会影响测试结果的准确性。建议使用以下的Nginx配置：
```nginx

  location /{
      add_header Content-Type text/plain;
      return 200 "ok";
  }
```

例如宝塔面板 Nginx 的测试配置
![image](/img/nginx.png)



# 2. WAF的配置

## 2.1 关闭CC防御
![image](/img/cc.png)



## 2.2 关闭拉黑IP功能
如果全局设置没有此项，就执行一下`btw 17` 更新一下

![image](/img/block.png)






# 3. 测试

```shell
root@debian:/tools/bl/blazehttp-master# ./build/blazehttp -t http://192.168.77.79
sending 100% |██████████████████████████████████████████████████████████████████████| (33877/33877, 1918 it/s) [17s:0s]
总样本数量: 33877    成功: 33877    错误: 0
检出率: 83.13% (恶意样本总数: 658 , 正确拦截: 547 , 漏报放行: 111)
误报率: 0.16% (正常样本总数: 33219 , 正确放行: 33165 , 误报拦截: 54)
准确率: 99.51% (正确拦截 + 正确放行）/样本总数 
平均耗时: 5.16毫秒
root@debian:/tools/bl/blazehttp-master# 

```