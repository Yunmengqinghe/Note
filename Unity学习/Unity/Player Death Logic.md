## 陷阱设置
+ 放置陷阱或敌人
+ 给陷阱添加碰撞体
+ 为陷阱添加 Traps 的 Tag

## 死亡动画
+ 添加控制器和动画[[Animation & Animator]]
+ 任何状态都可以变成死亡，将死亡动画与 Any State 做链接
+  在 Animator 窗口的左上角点击 Parameters , 点击+号选择 Trigger 类型，创建death
+ 将 Has Exit Time 的勾选去掉，在链接线上将 Transition Duration 设置为0
+ 点击 Animator 中动画之间的连接箭头，在 Inspector -> Conditions -> 添加前面创建的 Trigger 类型的death

## 死亡设置
+ 在人物上添加脚本[[Death Logic Script]]
+ 禁止人物移动
+ 重新加载界面

## 延时重启
+ 选择 Animation -> Player -> Death 动画
+ 点击 Preview 隔壁的红点，会记录我们对此对象做的任何修改，点击死亡动画后的部分，再勾选掉 Sprite Renderer
+ 点击想要开始重启的时间，选择 Preview 下长条形的按钮，在 Inspector 下选择 Function 里的脚本的方法，然后重启会在方法执行时候执行