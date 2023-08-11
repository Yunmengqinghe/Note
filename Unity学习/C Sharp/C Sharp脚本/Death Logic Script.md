## 死亡及其效果
+ 代码
```C#
using UnityEngine.SceneManagement;

private Animator anim;
private Rigidbody2D rb;

void Start()
{
	rb = GetComponent<Rigidbody2D>();
	anim = GetComponent<Animator>();
}

private void OnCollisionEnter2D(Collision2D collision)
{
	if(collision.gameobject.CompareTag("Trap"))
	{
		Die();
	}
}

private void Die()
{
	rb.bodyType = RigidbodyType2D.Static;
	anim.SetTrigger("death");
}

private void RestartLevel()
{
	SceneManager.LoadScene(SceneManeger.GetActiveScene().name);
	//重新加载当前界面
}
```