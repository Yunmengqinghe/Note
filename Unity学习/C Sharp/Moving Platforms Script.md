## 平台往复运动
+ 代码：WayPointFollower
```C#
[SerializeField] private GameObject[] waypoints;
private int currentWaypointIndex = 0;
[SerializeField] private float speed;

void Update()
{     	
	if(Vector2.Distance(waypoints[currentWaypointIndex].transform. position,transform.position) < .1f)
	{
		currentWaypointIndex++;
		if(currentWaypoint >= waypoints.Length)
		{
			currentWaypoint = 0;
		}
	}
	transform.position = Vector2.MoveTowards(transform.position,
waypoint[currentWaypointIndex].transform.position,Time.deltaTime * speed);
}
```

## 人物跟随移动
+ 代码（检测到接触平台就移动）：StickyPlatform
```C#
//不区分上面和边缘
private void OnCollisionEnter2D(Collision2D collision)
{
	if(collision.gameObject.name == "Player")
	{
		collision.gameObject.transform.SetParent(transform);
	}
}

private void OnCollisionExit2D(Collision2D collision)
{
	if(collision.gameObject.name == "Player")
	{
		collision.gameObject.transform.SetParent(null);
	}
}
```

```C#
//区分上面和边缘
private void OnTriggerEnter2D(Collider2D collision)
{
	if(collision.gameObject.name == "Player")
	{
		collision.gameobject.transform.SetParent(transform);
	}
}

private void OnTriggerExit2D(Collider2D collision)
{
	if(collision.gameObject.name == "Player")
	{
		collision.gameObject.transform.SetParent(null);
	}
}
```