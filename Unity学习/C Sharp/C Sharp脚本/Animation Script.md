## Setbool()切换动画
+ 代码实现
```C#
private float dirX = 0f;
private Animator anim;
private SpriteRenderer sprite;

void Start()
{
	anim = GetComponent<Animator>();
	//获取动画的组件
	sprite = GetComponent<SpriteRenderer>();
	//获取精灵纹理，后续反转动画图形
}

void Update()
{
	UpdateAnimationState();
}

private void UpdateAnimationState()
{
	if(diX > 0f)
	{
		anim.SetBool("running",true);
		sprite.flipx = false;//反转动画的X轴
	}
	else if(dirX < 0f)
	{
		anim.SetBool("running",true);
		sprite.flipx = true;
	}
	else
	{
		anim.SetBool("running",false);
	}
	//设置Bool值控制动画的转换
}
```

## 多动画切换
+ 代码
```C#
private enum MovementState { idle, running, jumping, falling }

void Update()
{
	UpdateAnimationState();
}

public void UpdateAnimationState()
{
	MovementState state;
	if(diX > 0f)
	{
		state = MovementState.running;
		sprite.flipx = false;//反转动画的X轴
	}
	else if(dirX < 0f)
	{
		state = MovementState.running;
		sprite.flipx = true;
	}
	else
	{
		state = MovementState.idle;
	}
	
	if(rb.velocity.y > .1f)
	{
		state = MovementState.jumping;
	}
	else if(rb.velocity.y < -.1f)
	{
		state = MovementState.falling;
	}
	
	anim.SetInterger("state",(int)state);
}
```

## 人物转身
```C#
//只控制Sprite转身，实际并没有转身
private SpriteRenderer sprite;
sprite.flipx = false;

//控制整个人物转身
transform.localRotation = Quaternion.Euler(0, y, 0);
```