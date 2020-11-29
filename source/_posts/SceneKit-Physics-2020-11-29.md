---
title: SceneKit-Physics 接触和碰撞
date: 2020-11-29 19:31:29
tags:
- IOS
- SceneKit
---

## SceneKit 接触和碰撞

#### categoryBitMask
###### 定义【物理身体】属于哪一种【类别】
- Every physics body in a scene can be assigned to one or more categories, each corresponding to a bit in the bit mask. 
  - `每个【物理身体】可以有一个或多个【类别】。对应【BitMask】中的某一位。`
- You define the mask values used in your game. Use this property together with the physicsShape and contactTestBitMask properties to define which physics bodies interact with each other and when your game is notified of interactions.
  - `和【物理形状】、【contactTestBitMask】一起，决定【物理身体】之间的交互以及触发的【通知】`
- The default value is static for static bodies and default for dynamic and kinematic bodies.
  - `【static身体】的默认值 = static `
  - `【dynamic and kinematic身体】的默认值 = default `

#### contactTestBitMask
###### 定义哪种【物理身体的类别】与自己发生【contact】交互

- When two physics bodies overlap, a contact may occur.
  - `当两个【物理身体】重叠时，【可能】会发生【contact】`
-  SceneKit compares the body’s contact mask to the other body’s category mask by performing a bitwise AND operation. If the result is a nonzero value, SceneKit creates an SCNPhysicsContact object describing the contact and sends messages to the contactDelegate object of the scene’s physics world. 
  - `本物体的【contactTestBitMask】与另一个物体【categoryBitMask】进行 【与】运算`
  - `如果返回【非零】:`
    1. 生成一个【SCNPhysicsContact】对象
    2. 发送一个消息给 【contactDelegate】对象

- For best performance, only set bits in the contact mask for interactions you are interested in.
  - `为了性能，仅为有必要的物体设置【contactTestBitMask】`

- For applications running in OS X v10.10 or iOS 8, this property’s value matches that of the collisionBitMask property—that is, SceneKit sends contact messages if and only if a collision occurs. For applications running in OS X v10.11 or iOS 9 or later, this property’s value defaults to zero and need not match the collision mask—that is, a pair of bodies generates contact messages whenever the bodies intersect, regardless of whether they collide or pass through one another.
  - `IOS8，只有【碰撞】了以后，才触发【contact】`
  - `IOS9以后：`
     1. 默认=0 ，（不与任何物体交互）
     2. 接触了就触发【contact】，与【碰撞】无关

#### collisionBitMask

###### 定义哪种【物理身体的类别】与自己发生【collision】碰撞

- When two physics bodies contact each other, a collision may occur. 
  - `当两个【物理身体】【contact】时，【可能】会发生【碰撞】`
- SceneKit compares the body’s collision mask to the other body’s category mask by performing a bitwise AND operation. If the result is a nonzero value, then the body is affected by the collision. Each body independently chooses whether it wants to be affected by the other body. For example, you might choose to avoid collision calculations that would make negligible changes to a body’s velocity.
  - `本物体的【collisionBitMask】与另一个物体【categoryBitMask】进行 【与】运算`
  - `如果返回【非零】:`
    1. 本物体发生【碰撞】
    2. 各物体之间的碰撞是独立的。
- The default value is all (a bit mask whose every bit is enabled), specifying that the body will collide with bodies of all other categories.
  - `默认值=0xFFFF, 即本物体与其他所有物体发生【碰撞】`



- When two physics bodies overlap, a contact may occur.
-  SceneKit compares the body’s contact mask to the other body’s category mask by performing a bitwise AND operation. If the result is a nonzero value, SceneKit creates an SCNPhysicsContact object describing the contact and sends messages to the contactDelegate object of the scene’s physics world. 
  - `一个物体的【contactTestBitMask】与另一个物体【categoryBitMask】进行 【与】运算`
  - `如果返回【非零】:`
    1. 生成一个【SCNPhysicsContact】对象
    2. 发送一个消息给 【contactDelegate】对象