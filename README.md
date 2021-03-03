# Unity
 
# First_Game(Bullet Avoid)

## Step 1.

������ ����Ǵ� ��(Plane)�� �ൿ ������ ����� ���� cube�� �̿��Ͽ� Ʋ�� �����.

<img src="plane.PNG" width=800 height=500>
* ���� ����Ƽ ȭ���Դϴ�

���⼭ ���� ������ Ʋ�� ũ��� ���Ƿ� ũ�⸦ ���Ͽ� �����Ͽ����ϴ�.

Plane �����

1. Hierarchyâ���� 3d create���� Plane�� �����.
2. Projectâ���� Material�� ���� �� ������ �����Ѵ�.
3. Projectâ�� �ִ� Plane ���� �ش��ϴ� Material�� plane�� �巡���Ѵ�.
4. Hierarchyâ���� Plane�� Ŭ���� �� Inspectorâ���� ������� ��ġ�� �����Ѵ�.

Ȳ�� ������ ���� Cube �����

1. Hierarchyâ���� 3d create���� Cube�� �����.(���� ������ �⺻�� ������� �����Ͽ���)
2. Hierarchyâ���� Cube�� Ŭ���� �� Inspectorâ���� Cube�� ũ��� ��ġ�� �����Ͽ� �����Ѵ�.

* Hierarchyâ���� ��ü���� �����ϱ� ���� �� ������ ���� �� ��� Cube�� Plane�� �־�ξ���.

## step 2.

�ش� ������ ���� �÷��̾� �����

<img src="player.PNG" width=800 height=500>

Player �����
1. Hierarchyâ���� 3d create���� Capsure�� �����.
2. �ش� Player�� ũ�⸦ ������ �� ������ �����Ѵ�.
3. ��ǻ�Ϳ��� Player�� �ν��� �� �ֵ��� Inspectorâ���� Tag�� Player�� ������ �ش�.
4. �ش� ���� �÷��̾�� �Ѿ��� ���ϸ鼭 �������� �ϱ� ������ �������� ���� �޾ƾ� �Ѵ� ���� Inspectorâ���� Add Component���� Rigidbody�� �߰��� �ش�, ���� Player�� Capsure�� �����߱� ������ �Ѿ����� �ʵ��� Rigidbodyâ�� �ִ� Constraints �ʵ忡�� �����ӿ� ������ �ɾ��ش�.
5. Player�� ������ �������� ������ �ֵ��� �ڵ��� �ؼ� �巡�� ���ݴϴ�, ���� �ڵ��� Player�ڵ��̰� ó������ if���� �̿��Ͽ� �ϳ��ϳ� �������� ���������� �����Ÿ� ������ ���� Horizontal, Vertical�޼��带 �̿��Ͽ� �ڵ��ߴ��� �ε巯�� �������� ���� �־���. 

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player : MonoBehaviour
{
    public Rigidbody playerRigidbody; // �̵��� ����� ������ٵ� ������Ʈ
    public float speed = 8f; //�̵� �ӷ�
    void Start()
    {
        playerRigidbody = GetComponent<Rigidbody>();
        // Capsure�� ������ Rigidbody ������Ʈ�� ã�� platerRigidbody�� �Ҵ��Ѵ�.
    }

    void Update()
    {
        float xInput = Input.GetAxis("Horizontal");
        float zInput = Input.GetAxis("Vertical");
        // ���� ���� �������� �����Ͽ� �����Ѵ�

        float xSpeed = xInput * speed;
        float zSpeed = zInput * speed;

        Vector3 newVelocity = new Vector3(xSpeed, 0f, zSpeed);
        playerRigidbody.velocity = newVelocity;

    }

        public void Die()
        {
            gameObject.SetActive(false); //gameObject = Player ���� ������Ʈ
        }
}
```


## step 3.

Player�� ���ؾ��� ź�˰� ź���� �߻�ü �����

<img src="bullet.PNG" width=800 height=500>
* �ش� ������ ���� ������ �۵���Ű�� ������ �����Դϴ�.


Bullet �����

1. Sphere�� ����� �ְ� ũ��� ��ġ�� ������ �ݴϴ�.
2. ������ ���� �����ݴϴ�.
3. Bullet ���� �������� ���� ���� ���󰡴� ����ü�̱� ������ Inspectorâ���� Rigidbody�� Add���ݴϴ�.
4. Bullet�� Player�� ��Ƴ��� ��Ȱ�� �ϱ� ������ ����� �����ϱ� ���� Inspectorâ���� Is Trigger�� Ȱ��ȭ ���� �ݴϴ�.
5. Bullet�� ������ ���� �Ѱ��� �ƴ� �������� ���󰡰� ���� �����δ� �߻�ü�� �� ����� ������ ������ �������ϴ� �Ѱ��Ѱ� �����ϱ� ����� ������ Bullet �������� ����� �Ѱ��� ������ �����Ͽ� �ٸ� Bullet���� ���� ������ �ɼ� �ֵ��� ������ �ݴϴ�.
6. Hierarchyâ�� �ִ� Bullet�� Projectâ���� �巡�� ���ָ� Projectâ�� Bullet �������� �����˴ϴ�.
7. BUllet�� �������� ���� BUllet�� �ش��ϴ� �ڵ��� �ؼ� �巡�� ���ݴϴ�.

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Bullet : MonoBehaviour
{
    public float speed = 8f; //ź�� �̵� �ӷ�
    private Rigidbody bulletRigidbody; //�̵��� ����� ������ٵ� ������Ʈ

    void Start()
    {
        
        bulletRigidbody = GetComponent < Rigidbody() >;
            //���� ������Ʈ���� Rigidbody ������Ʈ�� ã�� bulletRigidbody�� �Ҵ�
        bulletRigidbody.velocity = transform.forward * speed;
        //������ٵ��� �ӵ� = ���� ���� * �̵��ӷ�

        Destroy(gameObject, 3f);
    }

    void OntriggerEnter(Collider other)
    {
        if(other.tag == "Player")
        {
            PlayerController playerController = other.GetComponent<PlayerController>();
            // ���� ���� ������Ʈ���� PlaterController ������Ʈ ��������

            if (playerController != null)
            {
                playerController.Die();
            }
        }
    }
}

```






