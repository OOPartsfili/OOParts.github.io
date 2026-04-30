---
title: "Minimind精通+Agent实践"
collection: resources
type: "Resource"
permalink: /resources/Thisisyousee20260427
date: 2026-04-27
---

今天把项目里的Agent完善了下，同时进一步学习Minimind大模型算法原理

## Agent

Agent可以看下[小白debug](https://space.bilibili.com/302188068/?spm_id_from=333.788.upinfo.detail.click)的全面讲解，以下是harness engineer的最快速讲解
https://www.bilibili.com/video/BV1dpQTB3EXg?spm_id_from=333.788.videopod.sections&vd_source=c58c340875f11df8bb32588e63eaf494

项目Agent主要用到最简单的REACT框架，用了LANGCHAIN，单智能体推理，其实非常简陋

今天发现了这个AGENT的一个BUG，就是我换了一个模型API，它就因为输出格式不满足LANGCHAIN需求报错了，鲁棒性非常差。


## Minimind

一遍看理论一遍手撕，先把各个模块撕开。

包括ROPE,Yarn位置编码,  GQA理论与FFN


