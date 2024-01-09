## 一、第一种使用方式
### 安装Input System
+ 在 *Package Manager* 里选择右上角下拉框，切换成*Unity Registry*
+ 下载安装最新的 *Input System* 组件，在 *Asset* 下创建 *Setting* 目录，在目录下右键创建 *Input Actions*（文件名也为*Input Actions*）
+ 双击打开 *Input Actions*

### 动作绑定
1. 新建一个动作表 *GamePlay*
2. 新建一个 *Action*，创建为 *Move* 来负责人物的移动
+ 在右侧的 *Action Type* 选择 *Value* 类型
![[Input Action.png]]

+ 选择 *Control Type* 的类型为 *Vector2* ，即左右移动
![[ControlType.png]]

+ 添加按钮绑定
![[Unity InputSystem Button Binding.png]]
![[Unity InputSystem Vector2 Button Binding.png]]

3. 设置好后自动生成 *C Sharp* 类 
![[Unity InputSystem Automatically Generated Class.png]]
+ 接口函数
![[Unity InputSystem Interface IGameplayActions.png]]

### 函数编写
#### PlayInput类
```csharp
[CreateAssetMenu(menuName = "Player Input")]
public class PlayerInput : ScriptableObject, InputAction.IGamePlayActions
{
	public event UnityAction<Vector2> onMove = delegate {};
	public event UnityAction onStopMove = delegate {};
	protected InputActions inputActions;

	void OnEnable()
	{
		inputActions = new InputActions();
		inputActions.GamePlay.SetCallbacks(this);
	}
	
	void OnDisable()
	{
		DisableAllInputs();
	}
	
	public void DisableAllInputs()
	{
		inputActions.GamePlay.Disable();
	}

    public void EnableGamePlayInput()
    {
        inputActions.GamePlay.Enable();

        Cursor.visible = false;
        Cursor.lockState = CursorLockMode.Locked;
    }

	public void OnMove(InputAction.CallbackContext context)
	{
		//按下按键
		if(context.phase == InputActionPhase.Performed)
		{
			onMove.Invoke(context.ReadValue<Vector2>());
		}

		if(context.phase == InputActionPhase.Cancled)
		{
			onStopMove.Invoke();
		}
	}
}
```

+ 创建 *PlayerInput* , 命名为 *Player Input*
![[Creat PlayerInput Object.png]]

+ 将 *Player Input* 应用到 *Player*类 中
#### Player类
```csharp
public class Player : MonoBehaviour
{
	[SerializeField] PlayerInput input;
	public float moveSpeed;
	private Rigidbody2D rb;
	private void Start()
	{
	    rb = GetComponent<Rigidbody2D>();
	    input.EnableGamePlayInput();
	}
	
	public void OnEnable()
	{
	    input.onMove += Move;
	    input.onStopMove += StopMove;
	}
	
	public void OnDisable()
	{
	    input.onMove -= Move;
	    input.onStopMove -= StopMove;
	}
	
	public void Move(Vector2 moveInput)
	{
	    Vector2 moveAmont = moveInput * moveSpeed;
	    rb.velocity = moveAmont;
	}
	
	public void StopMove()
	{
	    rb.velocity = Vector2.zero;
	}
}


```

## 二、第二种使用方式
### 基本设置
+ 安装 *Input System*
+ 设置使用的输入系统 *Edit* -> *Package Settings*
![[Unity InputSystem Apply Setting.png]]

### 动作绑定
+ 绑定基本动作
![[Unity InputSystem Movement Binding.png]]

+ 设置控制方案
![[Unity InputSystem Contro lSchemes Setting.png]]

+ 为不同方案按钮进行选择
![[Unity InputSystem Botton Scheme Chose.png]]

### 组件设置
+ 为角色添加 *Player Input* 组件
![[Unity PlayerInput Component.png]]

+ 将 *Actions* 应用好，*Default Scheme* 设置为想要的对象
+ 将 *Behabior* 设置为 *Invoke Unity Events*
