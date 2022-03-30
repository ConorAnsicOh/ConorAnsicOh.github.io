---
layout: single
title: "[Conor] Unity C# 용어 설명 ( Unity description )"
description : "useful useful usefulllllll"
tags : [Algorithm]
comments : true
published : true
categories : Unity description useful
classes : wide
---

### ⊙Explanation of terms commonly used in Unity - Update Whenever I use. ( 유니티에서 많이 쓰이는 용어 설명 )

#### ○ Window

| Term      | Explain                           |
| --------- | --------------------------------- |
| Scene     | 영화의 장면 장면을 생각하면 된다. |
| Inspector | 오브젝트 세부 설정                |
|           |                                   |

#### ○ Object Inspector

| Term               | Explain                                                      |
| ------------------ | ------------------------------------------------------------ |
| Mesh Renderer      | 오브젝트 질감 설정                                           |
| Global Coordinates | 글로벌 좌표 ( 절대 좌표 ) - Scene에서 x버튼을 이용해 변경가능 |
| Local Coordinates  | 로컬 좌표 ( 상대 좌표 ) - Scene에서 x버튼을 이용해 변경가능하고<br /> 현재 보는 방향기준이다. |
|                    |                                                              |

#### ○ Et cetera

| Term | Explain                                                      |
| ---- | ------------------------------------------------------------ |
| Play | 씬을 실행시킨다. <br />( 주의사항 : 실행되고있을때 벌어지는 모든 수정사항은 플레이 종료후에 원상복귀 됨을 반드시 인지할 것. ) |
|      |                                                              |

### ○ Unity Object Components

| Components | Term                             | Explain                                                      |
| ---------- | -------------------------------- | ------------------------------------------------------------ |
| Rigidbody  | Mass                             | 물체 질량 (kg 단위)                                          |
|            | Drag                             | 힘을 가해 움직일 때 공기의 저항 수치 ( 0은 없음 무한대는 즉시 움직이지 않음 ) |
|            | Angular Drag                     | 회전할 때 공기의 저항 수치 ( 0은 없음 )                      |
|            | Use Gravity < Check Box >        | 중력의 영향 받는 여부                                        |
|            | Is Kinematic < Check Box >       | HingeJoint 가 연결된 Rigidbody를 애니메이션 할때 사용하면 좋음 |
|            | Interpolate < Drop Box >         | 움직임에 경련이 일어나는지 여부                              |
|            | Collision Detection < Drop Box > | 통과되는 현상 방지의 상세 지정                               |
|            | Constraints                      | RigidBody의 움직임을 좌표로 제한함.                          |
|            | Info                             | 정보나열                                                     |

