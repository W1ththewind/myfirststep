# 是时候开始真正的进步了
## 入职第一周
> - Unity Coroutine: 
> ```C#
>   //异步等待，开始协程运行的同时，原代码继续向下运行
>   IEnumorator _myCo;  //声明后赋Function，方便使用StartCoroutine()与StopCoroutine()控制
>   _myCo = MyCo(); //需要注意，调用完_myCo后，需要重新赋Funciton
>   private IEnumorator MyCo()
>   //若直接使用StartCoroutine传入MyCo()，可以开始，但无法使用StopCoroutine停止协程，因为无法找到明确的对象
>   {
>       yield return new wait();
>       ... //funciton代码
>   }
> ```
> - [SerializeField]写于变量前，可将protected、private变量在Unity的Editor中呈现，并进行操作 
> - [Menuitem("按钮")]后接function，可以实现Unity的Editor中按钮调用function 
> - Unity中Animation Event的调用时间，实际为上一帧动画结束的时刻，调用时SpriteRender还显示为上一帧的Sprite 
> - LayerMask 不同层级之间是bit移位的关系 00000101表示LayerMask 3和1层：
> ```C#
>   int Layer1 = 3;
>   int Layer2 = 5;
>   int LayerMask1 = 1 << Layer1;   //生成Layer1对应的Mask 2进制表示为00000100
>   int LayerMask2 = 1 << Layer2;   //2进制表示为00010000
>   int CombinedMasks = LayerMask1 | LayerMask2;    //Mask之间需使用 或(or)运算
>   //设定完成LayerMask之后可根据具体需要进行下一步操作：
>   if(Physics.RayCast(fromPosition, direction, Mathf.Infinity, CombinedMasks))
>   {
>       ... //当cast a Ray onto CombinedMasks，do sth
>   }
> ```
> - C# 运算符：
> ```C#
>   // ?. ：在运行右侧语句之前会先判断左侧是否为NULL，如果为NULL，则不执行右侧
>   // => :称为lambda表达式，表示一种委托，如：x => x * x; 会将x * x的结果返回给 X
>   //      也可以多个参数委托：（x ,y) => x + y; (0个参数委托时也需要使用括号：()=>)
>   //      =>后接一行代码会隐式添加 return，所以上式实际是{ return x + y;}
>   //      还可以委托复杂操作： x => { do sth; return sth }; 
>   // == ：可用于判断List是否完全相等（存疑
> ```
> - 面向对象编程？
> ```C#
>   //抽象：将某种对象建模成为类，以定义其种种行为、特性等等
>   //封装：在类中隐藏属性，仅开放公共函数以进行访问
>   //继承：根据现有的base class，创建同类型的更具体class，继承的class具有基类行为、特性（可override）
>   //多态：即在继承class过程中的override
>   public class Action //将动作抽象成类
>   {
>        public float weight;
>        public virtual void Move(){}   //虚方法，可在继承类中重写
>   }
>   public class Walk: Action //走动，继承动作
>   {
>       public new float weight;    //利用new关键字隐藏基类中的成员
>       public float Speed{get; private set};     //get、set增加对读写的控制(暂不甚解)
>       public override void Move()   //重写Move
>       {
>           ...// do sth, 可在此处访问_speed
>       }
>   }
> ```
---
## 入职第二三周
上周好像没有意识到休息就过去了。。既然如此，就在今天把这两周一起retro一下吧 
> - 上周work内容！ zombie关卡反复修改，达到勉强完整的地步 
> - 本周work：AutoZombie移动sync优化，Gas替换Arrow，新小关卡与复原初步实现 
> - 本周遗留问题： 复原表现效果、ZombieLift还原方案 
--- 
> - Input System Package: InputMap的简易使用 
> - Editor与EditorWindow类用以扩展编辑器 
```C#
public class DiyEditor: Editor
{
    public override void OnInspectorGUI()
    {
        ···//扩展Inspector
    }

     public void OnSceneGUI()
    {
        ··· //在Scene中定义控件等
    }

    ···
}

public class DiyEditor: EditorWindow
{
    [MenuItem("Window/DiyEditor")]  //添加菜单项
    static void Init()
    {
        DiyEditor _myWindow = EidtorWindow.GetWindow(typeof(DiyEditor));
        _myWindow.Show();
        //创建自定义窗口
    }

    void OnGUI()
    {
        ···//定义Editor窗口内的控件与功能
    }

    ···
}
```
> - 利用ScriptableObject实现数据持久化或存档（使用Manager管理ScriptbleObject对象），也可使用DontDestroyOnload(this)，以在关卡Reload后不丢失数据 
> - 
