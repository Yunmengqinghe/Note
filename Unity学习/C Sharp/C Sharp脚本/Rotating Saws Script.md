## 旋转
+ 代码
```C#
[SerializerField] private float speed;

void Update()
{
	transform.Rotate(0, 0, 360 * speed * Time.deltatime);
	//Time.deltatime是一个值，表示一帧的间隔时间
}
```