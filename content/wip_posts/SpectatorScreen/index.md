---
title: Spectator Screens in Unreal
date: '2019-01-05'
---

Set Spectator Screen Mode, Set Specator Screen Texture. Render Texture. 2D Capture. I put the script in the Level Blueprint.

### This should show up now....

Here's a code snippet.
```csharp{numberLines:true}
function test() {
  console.log("notice the blank line before this function?");
}
```


And another
Here's a code snippet.

```csharp{numberLines:true}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerPlatformerController : PhysicsObject {

    public float maxSpeed = 7;
    public float jumpTakeOffSpeed = 7;

    private SpriteRenderer spriteRenderer;
    private Animator animator;

    // Use this for initialization
    void Awake ()
    {
        spriteRenderer = GetComponent<SpriteRenderer> ();
        animator = GetComponent<Animator> ();
    }

    protected override void ComputeVelocity()
    {
        Vector2 move = Vector2.zero;

        move.x = Input.GetAxis ("Horizontal");

        if (Input.GetButtonDown ("Jump") && grounded) {
            velocity.y = jumpTakeOffSpeed;
        } else if (Input.GetButtonUp ("Jump"))
        {
            if (velocity.y > 0) {
                velocity.y = velocity.y * 0.5f;
            }
        }

        bool flipSprite = (spriteRenderer.flipX ? (move.x > 0.01f) : (move.x < 0.01f));
        if (flipSprite)
        {
            spriteRenderer.flipX = !spriteRenderer.flipX;
        }

        animator.SetBool ("grounded", grounded);
        animator.SetFloat ("velocityX", Mathf.Abs (velocity.x) / maxSpeed);

        targetVelocity = move * maxSpeed;
    }
}
```
