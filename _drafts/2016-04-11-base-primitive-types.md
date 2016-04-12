---
layout: post
title: 기본 도형 타입들 Base primitive types(topology)
date: 2016-04-05
categories: Graphic Programming
---

Point List
-----
아래의 이미지는 렌더링된 포인트 리스트를 보여줍니다.

![렌더링](https://i-msdn.sec.s-msft.com/dynimg/IC412648.png)

아래의 코드는 포인트 리스트를 출력하기 위해 버택스를 생성하는 코드입니다.
{% highlight C++ %}
struct CUTOMVERTEX {
	float x, y, z;
};

CUSTOMVERTEX vertices[] = {
	{ -5.0, -5.0, 0.0 },
	{  0.0,  5.0, 0.0 },
	{  5.0, -5.0, 0.0 },
	{ 10.0,  5.0, 0.0 },
	{ 15.0, -5.0, 0.0 },
	{ 20.0,  5.0, 0.0 }
}
{% endhighlight %}


또한 아래의 코드는 Direct3D 9의 `IDirect3DDevice9::DrawPrimitive`를 이용해 포인트 리스트를 렌더링하는 방법을 보여줍니다
{% highlight C++ %}
d3dDevice->DrawPrimitive(D3DPT_POINTLIST, 0, 6);
{% endhighlight %}


Line List
-----

Line Strip
-----

Triangle List
-----

Triangle Strip
-----