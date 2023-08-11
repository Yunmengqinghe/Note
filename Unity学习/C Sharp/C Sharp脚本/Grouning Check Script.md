## 跳跃次数的限制
+ 代码
```C#
private BoxCollider2D coll;
[SerializeField] private LayerMask jumpableGround;

void Start()
{
	coll = GetComponent<BoxCollider2D>();
}

void Update()
{
	if(Input.GetButtonDown("Jump") && isGround())
	{
		rb.velocity = new Vector2(rb.velocity.x, jumpSpeed);
	}
}

private bool isGround()
{
	return Physics2D.BoxCast(coll.bounds.center, coll.bounds.size, 0f, Vector2.down, .1f, jumpableGround);
	//触碰到地面则为true
}
```