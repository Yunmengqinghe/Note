## 切割图像
+ 将素材图片的Pixeis Per Unit改成16
+ 将Sprite Mode改成Multiple
+ 点击Sprite Editor -> Apply -> 放大Sprite Editor
+ 左上角点击Slice -> Type改成Grid By Cell Size（其他方式也可以，根据需要选用） -> 将Pixel Size改成 x:16 , y:16 -> 点击Slice -> 点击右上角的Apply

## Tilemap 
+ 在Hierarchy下右键选择 2D Object -> Tilemap -> Rectangular
+ Tilemap创建好后会在Grid目录下

## Tile-Palette
+ Window -> 2D ->Tile Palette
+ Create New Palette -> 命名 -> 保存在Asset目录下
+ 将切割好的素材拖进Tile Palette中，并创建一个新的文件夹来保存它
+ 调整图层(Additional Setting): 
	1、Sorting Layer中Add Sorting Layer（添加图层）,设置背景图层（比如Background层，Player层，Map层），层数越小优先级越小
	2、Order in Layer越小优先级越小
+ { 可以将 tile瓦片进行旋转

## 添加物体
+ 在Hierarchy下右键选择 2D Object -> Sprites -> Square
+ 将物体拖动到 Sprite Renderer 下的Sprite

## 刚体、碰撞体
+ 刚体的添加：在Inspector下选择Add Component，添加Rigidbody 2D，设置Gravity Scale（重力）

+ 碰撞体的添加：
	+ 物体的碰撞体：添加 Box Collider 2D，通过 Edit Collider调整碰撞体的大小
	+ Tilemap的碰撞体：添加 Tilemap Collider 2D 以及 Composite Collider 2D（把Tilemap分散的碰撞体合成大的碰撞体），将 Tilemap Colider 2D 下的 Used By Composite 勾选上，并且把自动添加的 Rigidbody 2D 设置为 Static（静态）

