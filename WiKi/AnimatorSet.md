####1.动画集有两种播放方式AnimatorSet——playSequentially,playTogether

* 按顺序播放


		AnimatorSet animatorSet = new AnimatorSet();
		animatorSet.playSequentially(tv1BgAnimator,tv1TranslateY,tv2TranslateY);
		animatorSet.setDuration(1000);
		animatorSet.start();

* 一起播放

	AnimatorSet animatorSet = new AnimatorSet(); animatorSet.playTogether(tv1BgAnimator,tv1TranslateY,tv2TranslateY); animatorSet.setDuration(2000); animatorSet.start();

animatorSet.setDuration(1000);指定的的每个动画的播放时间,会覆盖单个动画的播放时间

####2.自由设置动画顺序——AnimatorSet.Builder

	ObjectAnimator tv1BgAnimator = ObjectAnimator.ofInt(mTv1, "BackgroundColor", 0xffff00ff, 0xffffff00, 0xffff00ff); ObjectAnimator tv1TranslateY = ObjectAnimator.ofFloat(mTv1, "translationY", 0, 400, 0);
	
	AnimatorSet animatorSet = new AnimatorSet(); AnimatorSet.Builder builder = animatorSet.play(tv1BgAnimator); builder.with(tv1TranslateY); 
	animatorSet.start();

链式调用

	animatorSet.play(tv1TranslateY).with(tv2TranslateY).after(tv1BgAnimator);
builder.with():同时播放
builder.before():在传入对象之前播放
builder.after():在传入对象之后播放

####3.AnimatorSet 监听器

	public static interface AnimatorListener { /**
	
	当 AnimatorSet 开始时调用 */ void onAnimationStart(Animator animation);
	
	/**
	
	当 AnimatorSet 结束时调用 */ void onAnimationEnd(Animator animation);
	
	/**
	
	当 AnimatorSet 被取消时调用 */ void onAnimationCancel(Animator animation);
	
	/**
	
	当 AnimatorSet 重复时调用，由于 AnimatorSet 没有设置 repeat 的函数，所以这个方法永远不会被调用 */ void onAnimationRepeat(Animator animation); }

添加方法为：

	public void addListener(AnimatorListener listener);

例

	private AnimatorSet doListenerAnimation() {
	    ObjectAnimator tv1BgAnimator = ObjectAnimator.ofInt(mTv1, "BackgroundColor", 0xffff00ff, 0xffffff00, 0xffff00ff);
	    ObjectAnimator tv1TranslateY = ObjectAnimator.ofFloat(mTv1, "translationY", 0, 400, 0);
	    ObjectAnimator tv2TranslateY = ObjectAnimator.ofFloat(mTv2, "translationY", 0, 400, 0);
	    tv2TranslateY.setRepeatCount(ValueAnimator.INFINITE);
	
	    AnimatorSet animatorSet = new AnimatorSet();
	    animatorSet.play(tv1TranslateY).with(tv2TranslateY).after(tv1BgAnimator);
	    //添加 listener
	    animatorSet.addListener(new Animator.AnimatorListener() {
	        @Override
	        public void onAnimationStart(Animator animation) {
	            Log.d(tag, "animator start");
	        }
	
	        @Override
	        public void onAnimationEnd(Animator animation) {
	            Log.d(tag, "animator end");
	        }
	
	        @Override
	        public void onAnimationCancel(Animator animation) {
	            Log.d(tag, "animator cancel");
	        }
	
	        @Override
	        public void onAnimationRepeat(Animator animation) {
	            Log.d(tag, "animator repeat");
	        }
	    });
	    animatorSet.setDuration(2000);
	    animatorSet.start();
	    return animatorSet;
	}

在 AnimatorSet 中还有几个函数：

	//设置单次动画时长
	public AnimatorSet setDuration(long duration);
	//设置加速器
	public void setInterpolator(TimeInterpolator interpolator)
	//设置 ObjectAnimator 动画目标控件
	public void setTarget(Object target)