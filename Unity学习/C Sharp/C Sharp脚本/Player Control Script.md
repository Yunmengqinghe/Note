## 脚本的添加
+ 在Inspector下选择Add Component，添加 New script

## 物体变量
+ 使用变量来操作
+ 代码
```C#
private Rigidbody2D rb;

void Start()
{
	rb = GetComponent<Rigidbody 2D>();
}
//在开始时设置一个变量，后面可以只使用这个变量而不需要反复获取
	
void Update()
{
	if(Input.GetButtonDown("Jump"))
	{
		rb.velocity = new Vector2(rb.velocity.x, jumpSpeed);
	}
}
//GetButtonDown("")是获取一组对应的按键（比如Jump是space与上箭头），具体这组按键可以通过 Edit ->Project Setting ->Input Manager -> Axes 查看
```

## 跳跃 
+ 在Update下添加（先设置一个float类型的变量jumpSpeed来控制跳跃速度）
```C#
public float jumpSpeed;

void Update()
{
	if(Input.GetKeyDown("space"))
	{
		GetComponent<Rigidbody 2D>().velocity = new  Vector2(rb.velocity.x, jumpSpeed);
	}
}
//GetKey("")是持续获取键盘的输入，GetKeyDown("")是只获取一次键盘的输入
//GetComponent<>是控制Unity内的组件
//velocity是改变速度，Vector2是二维（X轴与Y轴）变量
```

## 左右移动
+ 在Update下添加（先设置一个float类型的变量jumpSpeed来控制移动速度）
```C#
public float moveSpeed;
private float dirX = 0f;

void Update()
{
	dirX = Input.GetAxisRaw("Horizontal");
	//GetAxis("")，GetAxisRaw("")返回一个-1~1之间的数字，可以在垂直移动和上下移动时候使用
	rb.velocity = new Vector2(dirX * moveSpeed,rb.velocity.y);
}
//GetAxis()和GetAxisRaw()的区别：
//GetAxis()的返回值m从0渐变为1或者-1;
//GetAxisRaw()的返回值从0直接变成1或者-1，没有渐变

```

## 摄像头跟随
+ 在Hierarchy下，将 Main Camera 拖动到人物身上，并且在 Inspector 下将 Transform 的 Position 的 X、Y 都设置成0
+ 冻结Z轴（防止发生旋转）
	在人物的 Rigidbody 2D 下点击 Constraints -> Freeze Rotation Z

## Unity中访问序列化的字段
+ 代码
```C#
[SerializeField] private float moveSpeed;
[SerializeField] private float jumpSpeed;
//可以在Unity内访问到，并且可以修改
```