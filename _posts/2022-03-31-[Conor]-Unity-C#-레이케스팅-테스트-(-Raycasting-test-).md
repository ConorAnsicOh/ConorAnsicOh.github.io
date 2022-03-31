---
layout: single
title: "[Conor] Unity C# 레이케스팅 테스트 ( Raycasting test )"
description : "raycasting"
tags : [Raycasting]
comments : true
published : true
categories : collision
cdlasses : wide
---

ㅁ

### ⊙ Unity Raycasting Test

#### ○Raycast Test - 1 ( Cannot penetrate an Object )

```` c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TestCollision : MonoBehaviour
{
    
    private void OnCollisionEnter(Collision collision)
    {
        // If you want to get an event here, you should keep in mind the following provisions. - 여기서 이벤트가 발생하게 하는 조건
        // 1) This or opponent should have "RigidBody" - 나 또는 상대에게 RigidBody가 있어야 한다. ( Is Kinematic : off )
        // 2) This or opponent should have "collider" - 나 또는 상대에게 Collider가 있어야 한다. ( Is Trigger : off )
        // 3) The opponent have "collider" - 상대에게 Collider가 있어야 한다. ( Is Trigger : off )

        Debug.Log($"Collision! @ {collision.gameObject.name}");
    }

    private void OnTriggerEnter(Collider other)
    {
        // If you want to get an event here, you should keep in mind the following provisions. - 여기서 이벤트가 발생하게 하는 조건
        // 1) Both Object have collider component - object둘 다 Collider가 있어야 한다.
        // 2) One of the two objects have to check "Is Trigger" - 둘 중 하나는 Is Trigger가 켜져있어야 한다.
        // 3) One of the two objects have "RigidBody" - 둘 중 하나는 RigidBody가 있어야 한다.

        Debug.Log($"Trigger! @ {other.gameObject.transform}");
    }

    void Start()
    {
        
    }

    void Update()
    {
        
        Vector3 look = transform.TransformDirection(Vector3.forward); // Function that converts world coordinates into local coordinates. - 로컬좌표계로 변경해줍니다.
        Debug.DrawRay(transform.position + Vector3.up, look * 10, Color.red);

        RaycastHit hit;

        if ( Physics.Raycast( transform.position + Vector3.up, look, out hit, 10 ) )
        {
            Debug.Log($"Raycast! {hit.collider.gameObject.name}!");
        }
    }
}

````



#### ○Raycast Test - 2 ( Can penetrate an Object )

````C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TestCollision : MonoBehaviour
{
    
    private void OnCollisionEnter(Collision collision)
    {
        // If you want to get an event here, you should keep in mind the following provisions. - 여기서 이벤트가 발생하게 하는 조건
        // 1) This or opponent should have "RigidBody" - 나 또는 상대에게 RigidBody가 있어야 한다. ( Is Kinematic : off )
        // 2) This or opponent should have "collider" - 나 또는 상대에게 Collider가 있어야 한다. ( Is Trigger : off )
        // 3) The opponent have "collider" - 상대에게 Collider가 있어야 한다. ( Is Trigger : off )

        Debug.Log($"Collision! @ {collision.gameObject.name}");
    }

    private void OnTriggerEnter(Collider other)
    {
        // If you want to get an event here, you should keep in mind the following provisions. - 여기서 이벤트가 발생하게 하는 조건
        // 1) Both Object have collider component - object둘 다 Collider가 있어야 한다.
        // 2) One of the two objects have to check "Is Trigger" - 둘 중 하나는 Is Trigger가 켜져있어야 한다.
        // 3) One of the two objects have "RigidBody" - 둘 중 하나는 RigidBody가 있어야 한다.

        Debug.Log($"Trigger! @ {other.gameObject.transform}");
    }

    void Start()
    {
        
    }

    void Update()
    {
        
        Vector3 look = transform.TransformDirection(Vector3.forward); // Function that converts world coordinates into local coordinates. - 로컬좌표계로 변경해줍니다.
        Debug.DrawRay(transform.position + Vector3.up, look * 10, Color.red);

        RaycastHit[] hits;
        hits = Physics.RaycastAll(transform.position + Vector3.up, look, 10);

        foreach ( RaycastHit hit in hits )
        {
            Debug.Log($"Raycast {hit.collider.gameObject.name}!");
        }
    }
}

````

#### ○Raycast Test - 3 ( Camera Raycast )

````C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TestCollision : MonoBehaviour
{
    
    private void OnCollisionEnter(Collision collision)
    {
        // If you want to get an event here, you should keep in mind the following provisions. - 여기서 이벤트가 발생하게 하는 조건
        // 1) This or opponent should have "RigidBody" - 나 또는 상대에게 RigidBody가 있어야 한다. ( Is Kinematic : off )
        // 2) This or opponent should have "collider" - 나 또는 상대에게 Collider가 있어야 한다. ( Is Trigger : off )
        // 3) The opponent have "collider" - 상대에게 Collider가 있어야 한다. ( Is Trigger : off )

        Debug.Log($"Collision! @ {collision.gameObject.name}");
    }

    private void OnTriggerEnter(Collider other)
    {
        // If you want to get an event here, you should keep in mind the following provisions. - 여기서 이벤트가 발생하게 하는 조건
        // 1) Both Object have collider component - object둘 다 Collider가 있어야 한다.
        // 2) One of the two objects have to check "Is Trigger" - 둘 중 하나는 Is Trigger가 켜져있어야 한다.
        // 3) One of the two objects have "RigidBody" - 둘 중 하나는 RigidBody가 있어야 한다.

        Debug.Log($"Trigger! @ {other.gameObject.transform}");
    }

    void Start()
    {
        
    }

    void Update()
    {

        // Local coordinates < - > World coordinates < - > Viewport < - > Screen ( 화면 )

        /// Debug.Log(Input.mousePosition); // Screen coordinates ( only x - axis, y - axis )
        // Results : This function is expressed in pixel numbers.

        /// Debug.Log(Camera.main.ScreenToViewportPoint(Input.mousePosition)); // Viewport coordinates ( only x - axis, y - axis )
        // Results : This function is expressed by converting coordinates into ratios.



        //This Function can replace the following functions.
        if ( Input.GetMouseButtonDown(0) )
        {

            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition); 

            Debug.DrawRay(Camera.main.transform.position, ray.direction * 100.0f, Color.red, 1.0f);

            RaycastHit hit;

            if ( Physics.Raycast(ray, out hit, 100.0f) )
            {
                Debug.Log($"Raycast Camera @ {hit.collider.gameObject.name}");
            }
        }


        //if (Input.GetMouseButtonDown(0))
        //{

        //    Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition); //This Function can replace the following functions.

        //    Vector3 mousePos = Camera.main.ScreenToWorldPoint(new Vector3(Input.mousePosition.x, Input.mousePosition.y, Camera.main.nearClipPlane));
        //    Vector3 dir = mousePos - Camera.main.transform.position;
        //    dir = dir.normalized;

        //    Debug.DrawRay(Camera.main.transform.position, dir * 100.0f, Color.red, 1.0f);

        //    RaycastHit hit;
        //    if (Physics.Raycast(Camera.main.transform.position, dir, out hit, 100.0f))
        //    {
        //        Debug.Log($"Raycast Camera @ {hit.collider.gameObject.name}");
        //    }
        //}

    }
}

````



