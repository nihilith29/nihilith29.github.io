---
layout: post
title: UniRx - Reactive Extensions for Unity
date: 2016-04-05
categories: UniRx

unirx:
 asset_store: http://u3d.as/content/neuecc/uni-rx-reactive-extensions-for-unity/7tT
 presentation: http://www.slideshare.net/neuecc/unirx-reactive-extensions-for-unityen
 ask_me_any_question: http://forum.unity3d.com/threads/248535-UniRx-Reactive-Extensions-for-Unity
 release_note: https://github.com/neuecc/UniRx/releases
---

*해당 문서는 GitHub의 UniRx 소개 페이지를 번역한 문서입니다.*

![UniRx](http://d2ujflorbtfzji.cloudfront.net/key-image/42fe86af-f6fb-4a7e-bfb6-4716121bab7e.jpg)

>What is UniRx?
>-----
>
>UniRx(Reactive Extensions for Unity) is a reimplementaion of the .NET Reactive Extentions. The Official Rx implementation is great but doesn't work on Unity and has issues with iOS IL2CPP compatibility. This library fixes those issues and adds some specific utilities for Unity. Supported platforms are PC/Mac/Android/iOS/WP8/WindowsStore/etc and the library is fully supported on both Unity 5 and 4.6.

**UniRx란?**
-----

UniRx(Reactive Extensions for Unity)는 .NET Reactive Extentions(Rx)의 재구현 입니다. 공식 Rx 구현은 훌륭하지만 유니티에서 iOS로 빌드시 IL2CPP의 문제가 있습니다. 이 라이브러리는 이러한 문제점을 고치고 유니티를 위한 몇몇 유틸리티가 추가되었습니다. 지원하는 플랫폼은 PC, Mac, Android, iOS, WP8, WindowsStore 등이며 유니티 버전 5 및 4.6을 완전히 지원합니다.

>UniRx is avilable on the [Unity Asset Store(FREE)]({{ page.unirx.asset_store }}) and presentation is [here]({{ page.unirx.presentation }}).

UniRx는 [유니티 에셋 스토어(무료)]({{ page.unirx.asset_store }})에서 이용할 수 있으며 프리젠테이션은 [여기]({{ page.unirx.presentation }})에 있습니다.

>Support thread on the Unity Forums: [Ask me any question]({{ page.unirx.ask_me_any_question }})

유니티 포럼에 지원 쓰레드가 있습니다: [무엇이든 물어보세요]({{ page.unirx.ask_me_any_question }})

>Release Notes, [see]({{ page.unirx.release_note }}).

릴리즈 노트는 [여기]({{ page.unirx.release_note }})를 참조해 주십시요.

>UniRx is Core Library(Port of Rx) + Platform Adaptor(MainThreadScheduler/FromCoroutine/etc) + Framework(ObservableTriggers/ReactiveProperty/PresenterBase/etc).

UniRx는 코어 라이브러리(Port of Rx) + 플랫폼 어뎁터(MainThreadScheduler/FromCoroutine/etc) + 프레임워크(ObservableTriggers/ReactiveProperty/PresenterBase/etc)로 이루어져 있습니다.

**Why Rx?**
-----

>Ordinarily, Network operations in Unity require the use of `WWW` and `Coroutine`. That said `Coroutine` is not good practice for asynchronous operations for the following (and other) reasons:
>
>1. Coroutines can't return any values, since its return type must be IEnumerator.
>2. Coroutines can't handle exceptions, because yield return statements cannot be surrounded with a try-catch construction.

일반적으로, 유니티에서 네트워크 조작은 `WWW`와 `Coroutine`을 필요로 합니다. 즉, `Coroutine`은 아래와 같은 이유(그리고 또다른)로 비동기 조작에서 좋은 해결책이 되지 않습니다:

1. `Coroutine`은 반드시 `IEnumerator`를 반환해야 함으로 어떠한 값도 반환 할 수 없습니다.
2. `Coroutine`의 `yield return`문은 `try-catch`로 감쌀 수가 없기 때문에 예외처리를 할 수 없습니다.

>This kind of lack of composability causes operations to be close-coupled, which often results in huge monolithic IEnumerators.

>Rx cures that kind of "asynchronous blues". Rx is a library for composing asynchronous and event-based programs using observable collections and LINQ-style query operators.

>The game loop (every Update, OnCollisionEnter, etc), sensor data (Kinect, Leap Motion, etc) are all types of events. Rx represents events as reactive sequences which are both easily composable and support time-based operations by using LINQ query operators.

>Unity is generally single threaded but UniRx facilitates multithreading for joins, cancels, accessing GameObjects, etc.

>UniRx helps UI programming with uGUI. All UI events(clicked, valuechanged, etc) can be converted to UniRx event stream.

**Introduction**
-----

>Great introduction to Rx article: The introduction to Reactive Programming you've been missing

훌륭한 Rx 소개 문서가 있습니다: 당신이 놓친 Reactive Programming 소개

>The following code implements the double click detection example from the article in UniRx:

다음 코드는 UniRx 문서의 더블 클릭 감지 구현 예제입니다.

{% highlight C# %}
var clickStream = Observable.EveryUpdate().
	Where(_ => Input.GetMouseButtonDown(0));
clickStream.Buffer(clickStream.Throttle(TimeSpan.FromMilliseconds(250))).
	Where(xs => xs.Count >= 2).
	Subscribe(xs => Debug.Log("DoubleClick Detected! Count: " + xs.Count));
{% endhighlight %}

>This example demonstrates the following features(in only five lines!)
>
>- The game loop (Update) as an event stream
>- Composable event streams
>- Merging self stream
>- Easy handling of time based operations