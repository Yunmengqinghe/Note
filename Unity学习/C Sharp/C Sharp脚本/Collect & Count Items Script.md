## 物体收集
+ 代码
```C#
private int cherries = 0;
private void OnTriggerEnter2D(Collider2D collision)
{
	if(collision.gameobject.CompareTag("Cherry"))
	{
		Destroy(collision.gameobject);
		cherries++;
		Debug.Log("Cherries: "+ cherries);
	}
}
```

## UI显示
+ 代码
```C#
using UniyEngine.UI;

[SerializeFileld] private Text cherriesText;

private void OnTriggerEnter2D(Collider2D collision)
{
	if(collision.gameobject.CompareTag("Cherry"))
	{
		Destroy(collision.gameobject);
		cherries++;
		cherriesText.text = "Cherries: " + cherries;
	}
}
```