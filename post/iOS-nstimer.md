---
title: NSTimer
tags:
  - NSTimer
  - 控件
id: 106
categories:
  - iOS
date: 2015-07-16 11:03:51
---

<span style="font-size: 18px;">转载自</span>

<span style="font-size: 18px;">NSTimer的使用方法</span>

<span style="font-size: 18px;">1、初始化</span>

<span style="font-size: 18px;">+ (NSTimer *)timerWithTimeInterval:(NSTimeInterval)ti target:(id)aTarget selector:(SEL)aSelector userInfo:(id)userInfo repeats:(BOOL)yesOrNo;</span>

<span style="font-size: 18px;">
</span>

<span style="font-size: 18px;">+ (NSTimer *)scheduledTimerWithTimeInterval:(NSTimeInterval)ti target:(id)aTarget selector:(SEL)aSelector userInfo:(id)userInfo repeats:(BOOL)yesOrNo;</span>

<span style="font-size: 18px;">
</span>

<span style="font-size: 18px;">注：不用scheduled方式初始化的，需要手动addTimer:forMode: 将timer添加到一个runloop中。</span>

<span style="font-size: 18px;">　　而scheduled的初始化方法将以默认mode直接添加到当前的runloop中.</span>

&nbsp;

<span style="color: rgb(51, 51, 51); font-family: Arial; font-size: 14px; line-height: 26px;"></span><span style="color: rgb(51, 51, 51); font-family: Arial; font-size: 14px; line-height: 26px; background-color: rgb(255, 255, 255);"></span>

<span style="font-size: 18px;">scheduledTimerWithTimeInterval:<span style="font-size: 13px; font-family: Courier;">(NSTimeInterval)</span>seconds &nbsp;</span>

<span style="font-size: 18px;">预订一个Timer,设置一个时间间隔。</span>

<span style="font-size: 18px;">表示输入一个时间间隔对象，以秒为单位，一个&gt;0的浮点类型的值，如果该值&lt;0,系统会默认为0.1</span>

<span style="font-size: 18px;">&nbsp;target:(id)aTarget</span>

<span style="font-size: 18px;">表示发送的对象，如<span style="font-size: 13px; font-family: &#39;Lucida Grande&#39;;">self</span></span>

<span style="font-size: 18px;">&nbsp;selector:(SEL)aSelector</span>

<span style="font-size: 18px;">方法选择器，在时间间隔内，选择调用一个实例方法</span>

<span style="font-size: 18px;">userInfo:(id)userInfo</span>

<span style="font-size: 18px;">此参数可以为nil，当定时器失效时，由你指定的对象保留和释放该定时器。</span>

<span style="font-size: 18px;">repeats:(BOOL)yesOrNo</span>

<span style="font-size: 18px;">当<span style="font-size: 13px; font-family: &#39;Lucida Grande&#39;;">YES</span>时，定时器会不断循环直至失效或被释放，当NO时，定时器会循环发送一次就失效。</span>

<span style="font-size: 24px;">invocation:(NSInvocation *)invocation</span>

&nbsp;

<span style="font-size: 18px;">举例：(不可控)</span>

<span style="font-size: 18px;">NSTimer *timer&nbsp;= [NSTimer&nbsp;scheduledTimerWithTimeInterval:10.0&nbsp;target:self&nbsp;selector:@selector(timerFired:)&nbsp;userInfo:nil&nbsp;repeats:NO];</span>

<span style="font-size: 18px;">或(可控制)</span>

<span style="font-size: 18px;">NSTimer *<span class="s1">myTimer</span><span class="s2">&nbsp;= [</span><span class="s3">NSTimer&nbsp;</span>timerWithTimeInterval<span class="s2">:</span><span class="s4">3.0&nbsp;</span>target<span class="s2">:</span><span class="s5">self</span>selector<span class="s2">:</span><span class="s5">@selector</span><span class="s2">(timerFired:)</span>userInfo<span class="s2">:</span><span class="s5">nil</span>repeats<span class="s2">:</span><span class="s5">NO</span><span class="s2">]</span><span class="s2">;</span></span>

<span style="font-size: 18px;"><span class="s2">[[</span><span class="s3">NSRunLoop &nbsp;</span>currentRunLoop<span class="s2">]</span>addTimer<span class="s2">:</span><span class="s1">myTimer</span>forMode<span class="s2">:</span><span class="s3">NSDefaultRunLoopMode</span><span class="s2">];</span></span>

<span style="font-size: 18px;">&nbsp;</span>

<span style="font-size: 18px;">2、触发（启动）</span>

<span style="font-size: 18px;">当定时器创建完（不用scheduled的，添加到runloop中后，该定时器将在初始化时指定的timeInterval秒后自动触发。</span>

<span style="font-size: 18px;"></span>

<span style="font-size: 18px;">可以使用-(void)fire;方法来立即触发该定时器；</span>

<span style="font-size: 18px;">注：You can use this method to fire a repeating timer without interrupting its regular firing schedule. If the timer is non-repeating, it is automatically invalidated after firing, even if its scheduled fire date has not arrived.</span>

<span style="font-size: 18px;">在重复执行的定时器中调用此方法后立即触发该定时器，但不会中断其之前的执行计划；</span>

<span style="font-size: 18px;">在不重复执行的定时器中调用此方法，立即触发后，就会使这个定时器失效。</span>

<span style="font-size: 18px;">&nbsp;</span>

<span style="font-size: 18px;">3、停止</span>

<span style="font-size: 18px;">- (void)invalidate;</span>

<span style="font-size: 18px;">这个是唯一一个可以将计时器从runloop中移出的方法。</span>

<span style="font-size: 18px;">&nbsp;</span>

<span style="font-size: 18px;">注：</span>

<span style="font-size: 18px;">NSTimer可以精确到50-100毫秒.</span>

<span style="font-size: 18px;">NSTimer不是绝对准确的,而且中间耗时或阻塞错过下一个点,那么下一个点就pass过去了.</span>