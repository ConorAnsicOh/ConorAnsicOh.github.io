---
layout: single
title: "[Conor] Unity C# 충돌 테스트 ( Collider )"
description : "Collider"
tags : [collider]
comments : true
published : true
categories : Unity-Exercise
classes : wide
---

### ⊙Collision Test

#### ○ Collision action matrix - Official

*-Collision detection occurs and messages are sent upon collision*

|                                          | Static Collider | Rigidbody | Kinematic Rigidbody Collider | Static aTrigger Collider | Rigidbody Trigger Collider | Kinematic Rigidbody Trigger Collider |
| ---------------------------------------- | --------------- | --------- | ---------------------------- | ------------------------ | -------------------------- | ------------------------------------ |
| **Static Collider**                      |                 | Y         |                              |                          |                            |                                      |
| **RigidBody Collider**                   | Y               | Y         | Y                            |                          |                            |                                      |
| **Kinematic Rigidbody Collider**         |                 | Y         |                              |                          |                            |                                      |
| **Static Trigger Collider**              |                 |           |                              |                          |                            |                                      |
| **Rigidbody Trigger Collider**           |                 |           |                              |                          |                            |                                      |
| **Kinematic Rigidbody Trigger Collider** |                 |           |                              |                          |                            |                                      |

*-Trigger messages are sent upon collision*

|                                          | Static Collider | Rigidbody | Kinematic Rigidbody Collider | Static aTrigger Collider | Rigidbody Trigger Collider | Kinematic Rigidbody Trigger Collider |
| ---------------------------------------- | --------------- | --------- | ---------------------------- | ------------------------ | -------------------------- | ------------------------------------ |
| **Static Collider**                      |                 |           |                              |                          | Y                          | Y                                    |
| **RigidBody Collider**                   |                 |           |                              | Y                        | Y                          | Y                                    |
| **Kinematic Rigidbody Collider**         |                 |           |                              | Y                        | Y                          | Y                                    |
| **Static Trigger Collider**              |                 | Y         | Y                            |                          | Y                          | Y                                    |
| **Rigidbody Trigger Collider**           | Y               | Y         | Y                            | Y                        | Y                          | Y                                    |
| **Kinematic Rigidbody Trigger Collider** | Y               | Y         | Y                            | Y                        | Y                          | Y                                    |

*※ That is why Collision Trigger Event is Hard to control.*

#### ○ Source

```` c#
````

