---
layout: post
title: UniRx - Reactive Extensions for Unity
date: 2016-04-05
categories: UniRx
---

해당 문서는 GitHub의 UniRx 소개 페이지를 번역한 문서입니다.


What is UniRx?

UniRx(Reactive Extensions for Unity) is a reimplementaion of the .NET Reactive Extentions. The Official Rx implementation is great but doesn't work on Unity and has issues with iOS IL2CPP compatibility. This library fixes those issues and adds some specific utilities for Unity. Supported platforms are PC/Mac/Android/iOS/WP8/WindowsStore/etc and the library is fully supported on both Unity 5 and 4.6.

UniRx(Reactive Extensions for Unity)는 .NET Reactive Extentions(Rx)의 재구현 입니다. 공식 Rx 구현은 훌륭하지만 유니티에서 iOS로 빌드시 IL2CPP의 문제가 있습니다. 이 라이브러리는 이러한 문제점을 고치고 유니티를 위한 몇몇 유틸리티가 추가되었습니다. 지원하는 플랫폼은 PC, Mac, Android, iOS, WP8, WindowsStore 등이며 유니티 버전 5와 4.6을 완전히 지원합니다.

UniRx is avilable on the [Unity Asset Store(FREE)](http://u3d.as/content/neuecc/uni-rx-reactive-extensions-for-unity/7tT) and presentation is [here](http://www.slideshare.net/neuecc/unirx-reactive-extensions-for-unityen).

UniRx는 [유니티 에셋 스토어(무료)](http://u3d.as/content/neuecc/uni-rx-reactive-extensions-for-unity/7tT)에서 이용할 수 있으며 프리젠테이션은 [여기](http://www.slideshare.net/neuecc/unirx-reactive-extensions-for-unityen)에 있습니다.

Support thread on the Unity Forums: [Ask me any question](http://forum.unity3d.com/threads/248535-UniRx-Reactive-Extensions-for-Unity)

유니티 포럼에 지원 쓰레드가 있습니다: [무엇이든 물어보세요](http://forum.unity3d.com/threads/248535-UniRx-Reactive-Extensions-for-Unity)

Release Notes, [see](https://github.com/neuecc/UniRx/releases).

릴리즈 노트는 [여기](https://github.com/neuecc/UniRx/releases)를 참조해 주십시요.

UniRx is Core Library(Port of Rx) + Platform Adaptor(MainThreadScheduler/FromCoroutine/etc) + Framework(ObservableTriggers/ReactiveProperty/PresenterBase/etc).

UniRx는 코어 라이브러리(Port of Rx) + 플랫폼 어뎁터(MainThreadScheduler/FromCoroutine/etc) + 프레임워크(ObservableTriggers/ReactiveProperty/PresenterBase/etc)로 이루어져 있습니다.


Introduction

Great introduction to Rx article: The introduction to Reactive Programming you've been missing

훌륭한 Rx 소개 문서가 있습니다: 당신이 놓친 Reactive Programming 소개

The following code implements the double click detection exammple from the article in UniRx:

UniRx 문서에 있는 더블 클릭 감지 구현 코드 예제를 보도록하죠.

{% highlight C# %}
var clickStream = Observable.EveryUpdate().
	Where(_ => Input.GetMouseButtonDown(0));
clickStream.Buffer(clickStream.Throttle(TimeSpan.FromMilliseconds(250))).
	Where(xs => xs.Count >= 2).
	Subscribe(xs => Debug.Log("DoubleClick Detected! Count: " + xs.Count));
{% endhighlight %}

This example demonstrates the following features(in only five lines!)

- The game loop (Update) as an event stream
- Composable event streams
- Merging self stream
- Easy handling of time based operations