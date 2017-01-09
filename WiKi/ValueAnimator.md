改变一系列属性值,过程中不断监听并给View重新设置属性

1.两个静态方法ofInt 与 ofFloat

	public static ValueAnimator ofInt(int... values)  
	public static ValueAnimator ofFloat(float... values)

2.实现变化监听

	ValueAnimator animator = ValueAnimator.ofFloat(0f,400f,50f,300f);  
	animator.setDuration(3000);  
	
	animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {  
	    @Override  
	    public void onAnimationUpdate(ValueAnimator animation) {  
	        Float curValueFloat = (Float)animation.getAnimatedValue();  
	        int curValue = curValueFloat.intValue();  
	        tv.layout(curValue,curValue,curValue+tv.getWidth(),curValue+tv.getHeight());  
	    }  
	});  
	animator.start(); 

####常用函数

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

例

	private ValueAnimator doRepeatAnim(){  
	   ValueAnimator animator = ValueAnimator.ofInt(0,400);  
	   animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {  
	       @Override  
	       public void onAnimationUpdate(ValueAnimator animation) {  
	           int curValue = (int)animation.getAnimatedValue();  
	           tv.layout(tv.getLeft(),curValue,tv.getRight(),curValue+tv.getHeight());  
	       }  
	   });  
	   animator.setRepeatMode(ValueAnimator.REVERSE);  
	   animator.setRepeatCount(ValueAnimator.INFINITE);  
	   animator.setDuration(1000);  
	   animator.start();  
	   return animator;  
	} 

####两个监听器

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

例

	private ValueAnimator doAnimatorListener(){  
	    ValueAnimator animator = ValueAnimator.ofInt(0,400);  
	
	    animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {  
	        @Override  
	        public void onAnimationUpdate(ValueAnimator animation) {  
	            int curValue = (int)animation.getAnimatedValue();  
	            tv.layout(tv.getLeft(),curValue,tv.getRight(),curValue+tv.getHeight());  
	        }  
	    });  
	    animator.addListener(new Animator.AnimatorListener() {  
	        @Override  
	        public void onAnimationStart(Animator animation) {  
	            Log.d("qijian","animation start");  
	        }  
	
	        @Override  
	        public void onAnimationEnd(Animator animation) {  
	            Log.d("qijian","animation end");  
	        }  
	
	        @Override  
	        public void onAnimationCancel(Animator animation) {  
	            Log.d("qijian","animation cancel");  
	        }  
	
	        @Override  
	        public void onAnimationRepeat(Animator animation) {  
	            Log.d("qijian","animation repeat");  
	        }  
	    });  
	    animator.setRepeatMode(ValueAnimator.REVERSE);  
	    animator.setRepeatCount(ValueAnimator.INFINITE);  
	    animator.setDuration(1000);  
	    animator.start();  
	    return animator;  
	} 

####取消监听

	/** 
	 * 移除 AnimatorUpdateListener 
	 */  
	void removeUpdateListener(AnimatorUpdateListener listener);  
	void removeAllUpdateListeners();  
	 /** 
	  * 移除 AnimatorListener 
	  */  
	void removeListener(AnimatorListener listener);  
	void removeAllListeners();

####其它函数

	/** 
	 * 延时多久时间开始，单位是毫秒 
	 */  
	public void setStartDelay(long startDelay)  
	/** 
	 * 完全克隆一个 ValueAnimator 实例，包括它所有的设置以及所有对监听器代码的处理 
	 */  
	public ValueAnimator clone() 

####设置差值器
animator.setInterpolator(new BounceInterpolator());  