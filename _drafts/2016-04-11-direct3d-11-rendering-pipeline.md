---
layout: post
title: 다이렉트3D 11의 렌더링 파이프라인
date: 2016-04-05
categories: Graphic Programming
comments: true
---

# **렌더링 파이프라인이란?**
렌더링 파이프라인(Rendering Pipeline)이란 가상 카메라에 비친 3차원 장면을 기준으로 2차원 이미지를 생성하는 일련의 단계들을 뜻합니다. 다이렉트3D 11의 렌더링 파이프라인은 -당연히- 다이렉트3D 10의 파이프라인을 기본으로 프로그래밍 가능한 쉐이더 단계들이 추가된 형태입니다.

다이렉트3D 11의 렌더링 파이프라인은 사실상 2개의 분리된 렌더링 파이프라인을 지원하며 각각 드로우 파이프라인(Draw pipeline: graphics rendering pipeline), 디스패치 파이프라인(Compute shader pipeline)입니다. 두개의 파이프라인은 기술적으로 느슨하게 연결되어 있으며, 

# Input Assembler 단계

# Vertex Shader 단계

# Hull 쉐이더 단계
 Hull 쉐이더는 패치당 한번씩 적용됩니다. Input assembler에서 패치와 함께 Hull 쉐이더를 사용할 수 있습니다. 

# Tessellator 단계

# Domain Shader 단계

# Geometry Shader 단계

# Stream Output 단계

# Rasterizer 단계

# Pixel Shader 단계

# Output Marger 단계
