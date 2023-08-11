## 添加枪械
+ 枪械切换与枪口方向代码
```C#
public GameObject[] guns;
public int gunNum;

public Vector2 input;
public Vector2 mousePos;

public Rigidbody2D rb;
public float speed;

private bool isRunning;
public Animator animator;

void Start()
{
    guns[0].SetActive(true);
    rb = GetComponent<Rigidbody2D>();
}

void Update()
{
    SwitchGun();
    ViewPointUpdate();
}

public void SwitchGun()
{
	if (Input.GetKeyDown(KeyCode.Q))
	{
		guns[gunNum].SetActive(false);
		if (--gunNum < 0)
		{
			gunNum = guns.Length - 1;
		}
		guns[gunNum].SetActive(true);
	}
	else if (Input.GetKeyDown(KeyCode.E))
	{
		guns[gunNum].SetActive(false);
		if (++gunNum > guns.Length - 1)
		{
			gunNum = 0;
		}
		guns[gunNum].SetActive(true);
	}
	//通过QE切换枪
}

public void ViewPointUpdate()
{   
	input.x = Input.GetAxisRaw("Horizontal");
	input.y = Input.GetAxisRaw("Vertical");
	rb.velocity = input.normalized * speed;//归一化获取方向
	
	mousePos = Camera.main.ScreenToWorldPoint(Input.mousePosition);
	
	if (mousePos.x > transform.position.x)
	{
		transform.rotation = Quaternion.Euler(new Vector3(0, 0, 0));
	}
	else
	{
		transform.rotation = Quaternion.Euler(new Vector3(0, 180, 0));
	}//切换人物、枪口朝向
}
```
+ 枪械设置代码
```C#
public float interval;
public float timer;

public GameObject bulletPerfab;
public GameObject shellPerfab;

public Transform firePos;
public Transform shellPos;

public Vector2 mousePos;
public Vector2 direction;

public Animator animator;

public float flipY;

protected virtual void Start()
{
	animator = GetComponent<Animator>();
	flipY = transform.localScale.y;
}

// Update is called once per frame
protected virtual void Update()
{
	mousePos = Camera.main.ScreenToWorldPoint(Input.mousePosition);
	Shoot();
	if (mousePos.x < transform.position.x)
	{
		transform.localScale = new Vector3(flipY, -flipY, 1);
	}
	else
	{
		transform.localScale = new Vector3(flipY, flipY, 1);
	}
}

protected virtual void Shoot()
{
	direction = (mousePos - new Vector2(transform.position.x, transform.position.y)).normalized;
	transform.right = direction;
	
	if (timer != 0)
	{
		timer -= Time.deltaTime;
		if (timer <= 0)
		{
			timer = 0;
		}
	}
	
	if (Input.GetMouseButton(0))
	{
		if (timer == 0)
		{
			Fire();
			timer = interval;
		}
	}
}

protected virtual void Fire()
{
	animator.SetTrigger("Shoot");
	//Instantiate(物体，位置，旋转)
	GameObject bullet = Instantiate(bulletPerfab, firePos.position, Quaternion.identity);

	float angle = Random.Range(-3f, 3f);
	bullet.GetComponent<Bullet>().SetSpeed(Quaternion.AngleAxis(angle, Vector3.forward) * direction);

	Instantiate(shellPerfab, shellPos.position, shellPos.rotation);
}
//枪的父类
```

```C#
private bool isShooting;
public LineRenderer lineRenderer;

protected override void Start()
{
	base.Start();
	lineRenderer = firePos.GetComponent<LineRenderer>();
}
protected override void Shoot()
{
	direction = (mousePos - new Vector2(transform.position.x, transform.position.y)).normalized;
	transform.right = direction;

	if(Input.GetMouseButtonDown(0))
	{
		isShooting = true;
		lineRenderer.enabled = true;
	}
	if(Input.GetMouseButtonUp(0))
	{
		isShooting = false;
		lineRenderer.enabled = false;
	}
	animator.SetBool("Shoot",isShooting);

	if(isShooting ==true)
	{
		Fire();
	}
}

protected override void Fire()
{   
	//Physics2D.Raycast(起点，方向，长度);
	RaycastHit2D hit2D = Physics2D.Raycast(firePos.position, direction,30);

	Debug.DrawLine(firePos.position, hit2D.point);

	lineRenderer.SetPosition(0, firePos.position);
	lineRenderer.SetPosition(1, hit2D.point);
}
//子类激光枪
```

+ 弹壳代码
```C#
public float speed;

public float stopTime;
public float fadeSpeed;

public Rigidbody2D rigidbody;
public SpriteRenderer sprite;

void Awake()
{
	rigidbody = GetComponent<Rigidbody2D>();
	sprite = GetComponent<SpriteRenderer>();
	//rigidbody.velocity = Vector3.up * speed;
	
	float angle = Random.Range(-30f, 30f);
	rigidbody.velocity = Quaternion.AngleAxis(angle, Vector3.forward) * Vector3.up * speed;
	StartCoroutine(Stop());
}

IEnumerator Stop()
{
	yield return new WaitForSeconds(stopTime);
	rigidbody.velocity = Vector2.zero;
	rigidbody.gravityScale = 0;

	while (sprite.color.a > 0)
	{
		sprite.color = new Color(sprite.color.r, sprite.color.g, sprite.color.b, sprite.color.a - fadeSpeed);
		yield return new WaitForFixedUpdate();
	}
	Destroy(gameObject);
}
```

+ 子弹代码
```C#
public float speed;

public Rigidbody2D rigidbody;

void Awake()
{
	rigidbody = GetComponent<Rigidbody2D>();
}

public void SetSpeed(Vector2 direction)
{
	rigidbody.velocity = direction * speed;
}

private void OnTriggerEnter2D(Collider2D collision)
{
	Destroy(gameObject);
}
```