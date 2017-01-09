由ValueAnimator派生,使用简单,是对控件的setter属性进行一系列的变化

	ObjectAnimator animator = ObjectAnimator.ofFloat(tv,"alpha",1,0,1);  
	animator.setDuration(2000);  
	animator.start(); 

基本属性有

	//1、透明度：alpha  
	public void setAlpha(float alpha)  
	
	//2、旋转度数：rotation、rotationX、rotationY  
	public void setRotation(float rotation)//z轴旋转  
	public void setRotationX(float rotationX)  
	public void setRotationY(float rotationY)  
	
	//3、平移：translationX、translationY  
	public void setTranslationX(float translationX)   
	public void setTranslationY(float translationY)  
	
	//缩放：scaleX、scaleY  
	public void setScaleX(float scaleX)  
	public void setScaleY(float scaleY) 

2.其它函数

	/** 
	 * 设置动画时长，单位是毫秒 
	 */  
	ValueAnimator setDuration(long duration)  
	/** 
	 * 获取 ValueAnimator 在运动时，当前运动点的值 
	 */  
	Object getAnimatedValue();  
	/** 
	 * 开始动画 
	 */  
	void start()  
	/** 
	 * 设置循环次数,设置为 INFINITE 表示无限循环 
	 */  
	void setRepeatCount(int value)  
	/** 
	 * 设置循环模式 
	 * value 取值有 RESTART，REVERSE， 
	 */  
	void setRepeatMode(int value)  
	/** 
	 * 取消动画 
	 */  
	void cancel()  
	（2）、监听器相关
	[java] view plain
	/** 
	 * 监听器一：监听动画变化时的实时值 
	 */  
	public static interface AnimatorUpdateListener {  
	    void onAnimationUpdate(ValueAnimator animation);  
	}  
	//添加方法为：public void addUpdateListener(AnimatorUpdateListener listener)  
	/** 
	 * 监听器二：监听动画变化时四个状态 
	 */  
	public static interface AnimatorListener {  
	    void onAnimationStart(Animator animation);  
	    void onAnimationEnd(Animator animation);  
	    void onAnimationCancel(Animator animation);  
	    void onAnimationRepeat(Animator animation);  
	}  
	//添加方法为：public void addListener(AnimatorListener listener)

3.插值器与 Evaluator

	/** 
	 * 设置插值器 
	 */  
	public void setInterpolator(TimeInterpolator value)  
	/** 
	 * 设置 Evaluator 
	 */  
	public void setEvaluator(TypeEvaluator value) 

