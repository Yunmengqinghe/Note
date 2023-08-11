## 音效控制
+ 脚本(在人物移动下添加)
```C#
[SerializeField] private AudioSource jumpSoundEffect;

void Update()
{
	
	if(Input.GetKeyDown("space"))
	{
		jumpSoundEffect.Play();//播放音效
		GetComponent<Rigidbody 2D>().velocity = new Vector2(rb.velocity.x,jumpSpeed);
	}
}
```

## 单例控制音效
+ 代码(soundManager)
```C#
	public static soundManager Instance;
    public AudioSource audioSource;
    public AudioClip jumpAudio, touchCherryAudio, hittedAudio;
    
    private void Awake()
    {
        Instance = this;
    }
    
    void Start()
    {
        audioSource = GetComponent<AudioSource>();
    }
    
    public void Jump()
    {
        audioSource.clip = jumpAudio;
        audioSource.Play();
    }
    
    public void TouchCherryAudio()
    {
        audioSource.clip = touchCherryAudio;
        audioSource.Play();
    }
    
    public void HittedAudio()
    {
        audioSource.clip = hittedAudio;
        audioSource.Play();
    }
	
	/*在别的脚本下调用时为
	soundManager.Instance.Jump();
	soundManager.Instance.TouchCherryAudio();
	soundManager.Instance.HittedAudio();
	*/
```