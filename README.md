# 才华横溢 workout_log 案例 8
```
cd workspace
rails new workout_log
cd workout_log
rails s
```
![image](https://ws3.sinaimg.cn/large/006tKfTcgy1fpgpkeefzwj31720zi1kx.jpg)

```
git init
git add .
git commit -m "initial commit"
git remote add origin https://github.com/shenzhoudance/workout_log.git
git push -u origin master
```
```
git checkout -b model workout
rails g model workout date:datetime workout:string mood:string length:string
rake db:migrate
```
![image](https://ws2.sinaimg.cn/large/006tKfTcgy1fpgptkw61gj31a00gqadi.jpg)
