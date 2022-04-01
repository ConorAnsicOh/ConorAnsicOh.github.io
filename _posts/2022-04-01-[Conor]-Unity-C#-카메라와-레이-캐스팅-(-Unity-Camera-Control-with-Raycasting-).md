---
layout: single
title: "[Conor] Unity C# 카메라와 레이 캐스팅 ( Unity Camera Control with Raycasting )"
description : "Unity Camera Control with Raycasting"
tags : [Raycasting]
comments : true
published : true
categories : Camera
classes : wide

---

### ⊙Unity Camera Control with Raycasting

#### ○ Deine.cs

```` C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Define
{
    public enum MouseEvent
    {
        Prese,
        Click,
    }

    public enum CameraMode
    {
        QuarterView,
    }
}

````

#### ○ PlayerController.cs

```` C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;


public class PlayerController : MonoBehaviour
{
    [SerializeField]
    float _moveSpeed = 10.0f;

    bool _moveToDest = false;
    Vector3 _destPos;

    void Start()
    {
        Managers.Input.KeyAction -= OnKeyboard; // 만약 미리 넣은게 있다면 삭제한다.
        Managers.Input.KeyAction += OnKeyboard; // InputManager에 Onkeyboard를 맡기는 것.
        Managers.Input.MouseAction -= OnMouseClicked; 
        Managers.Input.MouseAction += OnMouseClicked;
    }

    void Update()
    {
        if ( _moveToDest )
        {
            Vector3 dir = _destPos - transform.position;
            if ( dir.magnitude < 0.0001f ) // _destPos에서 포지션 값을 뺀 값이 0이 되지 않기 때문에 아주 작은 값으로 0을 대체함
            {
                _moveToDest = false;
            }
            else
            {
                // 아래 코드만으로 진행하면 이동할때 코드가 남은거리 계산을 못해서 와리가리 하는 현상이 일어나는데 이를 방지해주는 코드다.
                // If you proceed with only the code below, the code cannot calculate the remaining distance when moving, which prevents this.
                float moveDist = Mathf.Clamp(_moveSpeed * Time.deltaTime, 0.0f, dir.magnitude ); // dir.magnitude : 남은거리

                transform.position += dir.normalized * moveDist; // replace following code.
                ///transform.position = transform.position + dir.normalized * _moveSpeed * Time.deltaTime; /// = transform.position += dir.normalized * _moveSpeed * Time.deltaTime;
                // dir은 방향과 거리를 지니고 있다. 이 값에 normalized를 해줌으로 크기가 1짜리인 방향이 같은 벡터로 만들어줌으로 방향성의 크기만 지닐 수 있게 만든다.
                // 위 공식은 벡터 방향 * 속도 * 시간 = 벡터 거리 공식을 완성 시킨 것이다.


                // 캐릭터를 부드럽게 회전시키는 함수
                transform.rotation = Quaternion.Slerp(transform.rotation, Quaternion.LookRotation(dir), 20 * Time.deltaTime);

                // This code makes the player's movements stiff.
                ///transform.LookAt(_destPos);
            }
        }
    }

    void OnKeyboard()
    {
   
        if (Input.GetKey(KeyCode.W))
        {
            transform.rotation = Quaternion.Slerp(transform.rotation, Quaternion.LookRotation(Vector3.forward), 0.2f);
            transform.position += Vector3.forward * Time.deltaTime * _moveSpeed;
        }

        if (Input.GetKey(KeyCode.S))
        {
            transform.rotation = Quaternion.Slerp(transform.rotation, Quaternion.LookRotation(Vector3.back), 0.2f);
            transform.position += Vector3.back * Time.deltaTime * _moveSpeed;
        }

        if (Input.GetKey(KeyCode.A))
        {
            transform.rotation = Quaternion.Slerp(transform.rotation, Quaternion.LookRotation(Vector3.left), 0.2f);
            transform.position += Vector3.left * Time.deltaTime * _moveSpeed;
        }
        if (Input.GetKey(KeyCode.D))
        {
            transform.rotation = Quaternion.Slerp(transform.rotation, Quaternion.LookRotation(Vector3.right), 0.2f);
            transform.position += Vector3.right * Time.deltaTime * _moveSpeed;
        }

        _moveToDest = false;
    }

    void OnMouseClicked( Define.MouseEvent evt)
    {
        if ( evt != Define.MouseEvent.Click )
        {
            return;
        }

        Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);

        Debug.DrawRay(Camera.main.transform.position, ray.direction * 100.0f, Color.red, 1.0f);

        LayerMask mask = LayerMask.GetMask("Wall");

        RaycastHit hit;

        if (Physics.Raycast(ray, out hit, 100.0f, mask))
        {
            _destPos = hit.point;
            _moveToDest = true;
        }
    }
}

````

#### ※ Key Points

| Funtion              | Infomation                                                   |
| -------------------- | ------------------------------------------------------------ |
| @@@.magnitude        | Returns the length of this vector - 벡터의 값을 반환합니다.  |
| Mathf.Clamp          | Returns the given value if it is within the min and max range - 범위를 규정함 |
| transform.@@@        | It controls the settings for the movement of this object. - 이 객체의 움직임에 대한 설정을 관장한다. |
| transform.LookAt(aa) | Let this object be viewed in the vector coordinate direction of aa. -이 객체를 aa의 벡터 좌표로 바라보게 한다. |

#### ○ InputManager.cs

````c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class InputManager
{
    public Action KeyAction = null;

    public Action<Define.MouseEvent> MouseAction = null;

    bool _pressed = false;

    public void OnUpdate()
    {
        if (Input.anyKey && KeyAction != null )
        {
            KeyAction.Invoke();
        }

        if ( Input.GetMouseButton(0) ) // 0 : Left Mouse Button
        {
            MouseAction.Invoke(Define.MouseEvent.Prese);
            _pressed = true;
        }
        else
        {
            if ( _pressed )
            {
                MouseAction.Invoke(Define.MouseEvent.Click);
                _pressed = false;
            }
        }
    }
}
````

#### ○ CameraController.cs

```` C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraController : MonoBehaviour
{
    [SerializeField]
    Define.CameraMode _mode = Define.CameraMode.QuarterView;

    [SerializeField]
    Vector3 _delta = new Vector3(0.0f, 6.0f, -5.0f);

    [SerializeField]
    GameObject _player = null;

    void Start()
    {
        
    }

    // LateUpdate : Update After will do
    void LateUpdate()
    {
        if ( _mode == Define.CameraMode.QuarterView )
        {
            // 카메라가 가려질때 쓰면 좋은 코드
            RaycastHit hit;
            if ( Physics.Raycast(_player.transform.position, _delta, out hit, _delta.magnitude, LayerMask.GetMask("Wall")) )
            {
                float dist = (hit.point - _player.transform.position).magnitude * 0.8f; // hit.point : 카메라에서 닿은 물체 좌표, _player.transform.position : 플레이어의 벡터 좌표
                transform.position = _player.transform.position + _delta.normalized * dist; // 플레이어 벡터 좌표 + 방향 * 거리
            }
            else
            {
                transform.position = _player.transform.position + _delta;
                transform.LookAt(_player.transform); // 대상을 무조건 쳐다 보도록 만드는 함수
            }


        }

        
    }

    public void SetQuaterView(Vector3 delta)
    {
        _mode = Define.CameraMode.QuarterView;
        _delta = delta;
    }
}
````

