源码

	public class ArgbEvaluator implements TypeEvaluator {  
	    public Object evaluate(float fraction, Object startValue, Object endValue) {  
	        int startInt = (Integer) startValue;  
	        int startA = (startInt >> 24);  
	        int startR = (startInt >> 16) & 0xff;  
	        int startG = (startInt >> 8) & 0xff;  
	        int startB = startInt & 0xff;  
	
	        int endInt = (Integer) endValue;  
	        int endA = (endInt >> 24);  
	        int endR = (endInt >> 16) & 0xff;  
	        int endG = (endInt >> 8) & 0xff;  
	        int endB = endInt & 0xff;  
	
	        return (int)((startA + (int)(fraction * (endA - startA))) << 24) |  
	                (int)((startR + (int)(fraction * (endR - startR))) << 16) |  
	                (int)((startG + (int)(fraction * (endG - startG))) << 8) |  
	                (int)((startB + (int)(fraction * (endB - startB))));  
	    }  
	}

使用

方法一:

	ObjectAnimator animator = ObjectAnimator.ofInt(tv, "BackgroundColor", 0xffff00ff, 0xffffff00, 0xffff00ff);  
	animator.setDuration(8000);  
	animator.setEvaluator(new ArgbEvaluator());  
	animator.start();

方法二:

	ValueAnimator animator = ValueAnimator.ofInt(0xffffff00,0xff0000ff);  
	animator.setEvaluator(new ArgbEvaluator());  
	animator.setDuration(3000);  
	
	animator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {  
	    @Override  
	    public void onAnimationUpdate(ValueAnimator animation) {  
	        int curValue = (int)animation.getAnimatedValue();  
	        tv.setBackgroundColor(curValue);  
	
	    }  
	});  
	
	animator.start(); 