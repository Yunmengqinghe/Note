## 创建动画
+ 在资源目录下右键 Creat -> Animation ，将 Animation 命名
+ 将 Animation 拖到要创建动画的物体上面，此时目录下会出现一个 Animator Controller
+ Window -> Animation ->点击要创建动画的物体 -> 将资源拖动到上面
+ 设置采样率：Animation 窗口的右上角有三个点，点击再点击 Show Sample Rate
+ 重复播放：点击目录下创建的 Animation ，勾选 Loop Time

## 动画切换
+ Window -> Animation 打开窗口
+ 在 Animator 窗口的左上角点击 Parameters , 点击+号选择 Bool 类型，创建
+ 点击 Animator 中动画之间的连接箭头，将 Has Exit Time 的勾选去掉，再点击 Setting ，将 Transition Duration 设置为0
+ 点击 Animator 中动画之间的连接箭头，在 Inspector -> Conditions -> 添加前面创建的 Bool 类型的触发器

## 多动画切换
+ 在 Animator 窗口的左上角点击 Parameters , 点击+号选择 Int 类型，创建state
+ 点击 Animator 中动画之间的连接箭头，在 Inspector -> Conditions -> 添加 state ，选择 Equals ，再选择要切换的动画
+ 将 Has Exit Time 的勾选去掉，在链接线上将 Transition Duration 设置为0
+ 添加脚本[[Animation Script]]
