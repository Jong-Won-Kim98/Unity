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
7. BUllet�� BulletSpawner�� ���� �߻�Ǿ� Player�� ���̴� �������� �����ϸ� �����մϴ�.
8. BUllet�� �������� ���� BUllet�� �ش��ϴ� �ڵ��� �ؼ� �巡�� ���ݴϴ�.

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

    void OnTriggerEnter(Collider other)
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

BulletSpawner �����

1. Cylinder�� ����� ũ��� ��ġ�� ����ְ� ������ ������ �ݴϴ�.
2. BulletSpawner�� �ϴ����� �ֱ������� Bullet�� Player���� �߻��ϴ� ���� �����ϸ� �ش� ��ũ��Ʈ�� �����մϴ�.

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BulletSpawner : MonoBehaviour
{
    public GameObject bulletPrefab; // ź���� ���� ������
    public float spawnRateMin = 0.5f; // ���� ź�� ���� �ֱ�
    public float spawnRateMax = 3f; // �ִ� ���� �ֱ�

    private Transform target; // �߻��� ���
    private float spawnRate; // ���� �ֱ�
    private float timeAfterSpawn; // �ֱ� ���� �������� ���� �ð�

    void Start()
    {
        timeAfterSpawn = 0f; // ź���� �ϳ� ������ �� ���� �ð��� 0���� �ʱ�ȭ
        spawnRate = Random.Range(spawnRateMin, spawnRateMax); // ź�� �߻� �ֱ⸦ spawnRateMin�� spawnRateMax������ ���������� ����
        target = FindObjectOfType<PlayerController>().transform; // PlayerController������Ʈ�� ���� ��ü�� ��ǥ���� ����
    }

    // Update is called once per frame
    void Update()
    {
        timeAfterSpawn += Time.deltaTime; // ��ǻ�͸��� �ӵ��� �ٸ����� Update�� �����Ҷ� ���� �� ������ �ð� ������ ���Ž��� �ݴϴ�.

        if (timeAfterSpawn >= spawnRate)
        // timeAfterSpawn(���� �ֱ� ź���� ������ �����ð�)�� spawnRate(���� �ֱ�)���� ũ�ų� ������
        {
            timeAfterSpawn = 0f; // �����ð��� �����Ѵ�.
            GameObject bullet
                = Instantiate(bulletPrefab, transform.position, transform.rotation);
            // ���� bullet�� ������ bullet�� ��ġ�� ȸ���� ������ �ݴϴ�.
            bullet.transform.LookAt(target);
            // Ÿ��(Player)�� ���鿡�� bullet�� ���ϵ��� �����ݴϴ�.
            spawnRate = Random.Range(spawnRateMin, spawnRateMax);
            // ź�� ���� �ֱ⸦ spawnRateMin�� spawnRateMax������ ���������� ����
        }
    }
}

```

BulletSpawner�� �������� ����� ���� ������ BUlletSpawner�� 3���� ����� �ݴϴ�.
<img src="bulletspawner.PNG" width=800 height=500>

## step 4.

���� ���̵� ���̱�.

�Ѿ˸� ���ϱ�� ������ �ɽ��ϴٰ� �����Ͽ� ���̵��� �ø��� �ʹٴ� ������ ��� ����� �����ϴ� ���� �ٴ��� ȸ����Ű�� ����� �߻�ü�� �����̴� ����� ������ ���ҽ��ϴ� �켱 �ٴ��� ȸ����Ű�� �ڵ带 ¥������ �ϰڽ��ϴ�.

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Rotator : MonoBehaviour
{
    public float rotationSpeed = 60f;
    // 1�� 60�� ȸ�� �ϵ��� ����
    void Update()
    {
        transform.Rotate(0f, rotationSpeed, 0f);
    }
    // Rotate�޼��带 Ȱ���Ͽ� rotationSpeed�� �Ҵ��Ͽ� ������Ʈ �ǵ��� �����մϴ�.
}
```

- �� �ڵ�� ��ó�� �����Ͽ� ������ �ڵ����� �����غ� ��� Rotate�� Update�޼��忡 �Ҵ��Ͽ� 1�����ӿ� 60���� ȸ���ϵ��� �����Ǿ����ϴ�, �� ��ǻ�� ���� 1�ʴ� �� �������� ���ư����� �ٸ��� ������ �� ��ǻ�͸��� ȸ�� �ӵ��� �޶����� ������ ���� �������� �ð� ������ �����մϴ�.

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Rotator : MonoBehaviour
{
    public float rotationSpeed = 60f;

    void Update()
    {
        transform.Rotate(0f, rotationSpeed * Time.deltaTime, 0f);
    }
    // Time.deltaTime: �ʴ� �������� ����
}
```

Step 5.

���� �ٹ̱�

UI: ���ӿ����� ������Ʈ�� �ƴ� ������ ������Ʈ�� �ٸ� �������� �ٷ�� ��ü������ UI��ü������ �ڽ��� ��Ҹ� ���� ������Ʈ�� ����մϴ�.

�����ð� UI�����.
1. �켱 UI�� 2D�� �۾��ϴ°��� ���ϱ� ������ 2D�� ������ �ݴϴ�.
2. Hierarchyâ���� UI -> Text�� �����մϴ�.
3. Text�� Inspectorâ���� �����մϴ�.
4. ���������� Text�� ��ġ, ��Ʈ ũ��, �ؽ�Ʈ ����, ���� �����Ҽ� �ֽ��ϴ�. ��, ��Ʈ ũ�⸦ �����ϱ� ���ؼ��� ���� ������ Overflow�� ��������� ��Ʈ�� ©���� �ʰ� �״�� ��µ˴ϴ�.

���� ����� �ؽ�Ʈ �����.

1. �����ð� �ؽ�Ʈ�� ����Ͱ� ���������� UI���Ͽ� �ؽ�Ʈ�� �ϳ� �� �����մϴ�.
2. �������� Text�� ��ġ, ��Ʈ ũ��, �ؽ�Ʈ ����, ���� �����Ҽ� �ֽ��ϴ�. ��, ��Ʈ ũ�⸦ �����ϱ� ���ؼ��� ���� ������ Overflow�� ��������� ��Ʈ�� ©���� �ʰ� �״�� ��µ˴ϴ�.

�ְ��� �ؽ�Ʈ �����.

1. ���� ���� ������� �ؽ�Ʈ�� �ϳ� �߰��մϴ�.
2. �ְ��� �ؽ�Ʈ�� ���� ����� �ؽ�Ʈ�� �Բ� ��µǵ��� ���� ����� �ؽ�Ʈ�� �ڽ� ���Ϸ� �����մϴ�.
3. �������� Text�� ��ġ, ��Ʈ ũ��, �ؽ�Ʈ ����, ���� �����Ҽ� �ֽ��ϴ�. ��, ��Ʈ ũ�⸦ �����ϱ� ���ؼ��� ���� ������ Overflow�� ��������� ��Ʈ�� ©���� �ʰ� �״�� ��µ˴ϴ�.

���� �� �׽�Ʈ���� ������ ����� �� �� �ֵ��� �ڵ��� �ݴϴ�.

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    public GameObject gameoverText; // ���ӿ����� Ȱ��ȭ�� �ؽ�Ʈ(����� �ؽ�Ʈ, �ְ��� �ؽ�Ʈ)
    public Text timeText; // ���� �ð� ǥ���ϴ� �ؽ�Ʈ ������Ʈ
    public Text recordText; // �ְ� ��� ǥ���� �ؽ�Ʈ ������Ʈ

    private float surviveTime; // ���� �ð�
    private bool isGameover; //���ӿ��� ����

    void Start()
    {
        surviveTime = 0;
        isGameover = false;
    }

    void Update()
    {
        if (!isGameover) // �����ϴ� ����
        {
            surviveTime += Time.deltaTime; // �ð� ����
            timeText.text = "Time:" + (int)surviveTime; // ���� �ð� timeText�� ǥ��
        }
        else
        {
            if (Input.GetKeyDown(KeyCode.R))
            {
                SceneManager.LoadScene("SampleScene");
            /* using UnityEngine.SceneManagement�� ���� �ִ� ����� ������ 
            ��, SampleScene�� �ı��ϰ� ���ο� SampleScene�� �������Ƿ� ������ ������մϴ�. */
            }
        }        
        
    }

    public void EndGame()
    {
        isGameover = true;
        // ������ ������ ���
        gameoverText.SetActive(true);
        // ���ӿ��� �ؽ�Ʈ Ȱ��ȭ\
        float bestTime = PlayerPrefs.GetFloat("BestTime");
        // �̹� bestTime���� ����� ��� ��������

        if(surviveTime > bestTime)
        {
            bestTime = surviveTime;
            PlayerPrefs.SetFloat("BestTime", bestTime);

        }
        recordText.text = "best Time:" + (int)bestTime;
    }
}
```
������ �ؽ�Ʈ�� �� ����� �ϴ��� Ȯ���ϰ� Player��ũ��Ʈ�� �Ѿ Die �޼��忡 GameManager��ũ��Ʈ�� �߰��� �ݴϴ�.

Gamemanager��ü �����
1. Hierarchyâ���� �� ��ü�� ����� Gamemaneger��ũ��Ʈ�� �巡�� ���ݴϴ�.
2. Gamemanager��ü�� Ŭ���� �� Inspectorâ���� ������ ��ɿ� �ش��ϴ� �ؽ�Ʈ���� �������ݴϴ�.
3. �� �׸�ó�� ��� �ؽ�Ʈ���� �� ����� �Ҽ� �ִ°��� Ȯ���Ҽ� �ֽ��ϴ�.

<img src="Finish.PNG" width=800 height=500>


----
----

# Second_Game(Tile Map)

* �̹� ������ ������ �ִ� ���� �ҽ��� �̹��� ���ϵ��� ������ ����� ���ҽ��ϴ�.

Step1.

���� Start_Line�� Dead_Line �����.

���� ���� �����

1. ������ ���� �ҽ����� Platform_Long�� ������ Hierarchyâ���� ������ �ϳ��� ������Ʈ�� ��������ϴ�.
2. ���� Dead Line�� ������ �ϱ⶧���� ������ Position�� �����մϴ�.
3. Platform_Long�� Box Collider 2D�� �߰��մϴ�.
- Box Collider 2D�� �ٸ� Collider��Ұ� �ִ� ��ü�� �浹�� �Ͼ���� �ϴ� ������Ʈ�Դϴ�.
<img src="Long.PNG" width=800 height=200>

Dead Line �����

1. Dead Line�� �⺻ ������ �÷��̾ ���ǿ� �������� ���ϰ� ���� �������� �浹�� �����ϸ� �״°��� �⺻ ������ �Ͽ����ϴ�.
2. Hierarchyâ���� �� ������Ʈ�� �����Ͽ� �±׸� Dead�� �ٲ��ݴϴ�.
3. ��ġ�� ���Ǻ��� ������ ������ �� �ؿ��ִ� ������ ����� �����Ƿ� ������ ��ġ�� �������ݴϴ�.
4. Box Collider 2D ������Ʈ�� �߰��մϴ�
5. Box Collider 2D ������Ʈ�� Is Trigger�� üũ�Ͽ� �ٸ� ������Ʈ���� �浹�� �����Ҽ� �ֵ��� �����մϴ�.
6. Dead Line�� ���̴� ��� ���� ���̿� �����ؾ� �ϹǷ� �ִ��� ��� �������ְ� ���߿� ���̰� ������ ��� �÷��ݴϴ�.
 <img src="Dead Line.PNG" width=800 height=200>

Step2.

Player �����.

1. ù ȭ�鿡�� ���̴� Player�� ��ũ��Ʈ�� slice�ؼ� Hierarchyâ�� �߰��� �մϴ�.
2. Hierarchyâ�� �߰��� Player ������Ʈ�� Rigidbody ������Ʈ�� �߰��Ͽ� �浹�� �����մϴ�.
3. Circle Collider 2D������Ʈ�� �߰��Ͽ� Player�� �� �𼭸��� ���������� �ε巴�� Ÿ�� �ö󰡵��� �߰��� �ݴϴ�.
4. Audio Source ������Ʈ�� �߰��Ͽ� Player�� �ൿ�� ���� ��� ������ �־��ݴϴ�.
5. Slice��Ų Player���� animation���� ��� �����Ͽ� Player�� �������� ����� �ݴϴ�.
6. animationâ���� Player�� �������� �ʹ� ������ �������� �����ϸ� Samples�� ������ �ݴϴ�. 
7. ���� ������� Jump�� Die�� �������� �����Ͽ� �����մϴ�.

- ����Ƽ 2D������ Single ��������Ʈ�� �������� �� Multiple ��������Ʈ�� ������ �����մϴ�, �� �ϳ��� Multiple ��������Ʈ�� �������� Single ��������Ʈ�� �߶� ����Ҽ��� �ֽ��ϴ�.

Step3.

Player �� ����.

 1. Animatorâ�� �ش� ������Ʈ�� Animation ��Ʈ�ѷ��� ���µ��� ǥ���ϴ� â�Դϴ�.
 2. Animatorâ�� �� ���� Player�� Animation ��Ʈ���� �������� ������ �ݴϴ�.
 3. Animator������ ������ Animation���� ���콺�� �巡�� ���ݴϴ�.
 4. ������ ȭ��ǥ�� Ŭ���ϸ� �ش� �������� �ϴ� ������ ������ ������ �� �ֽ��ϴ�.
 5. Die�� Dead Line�� �浹�� ���� ��� �ױ� ������ Trigger�� ������ �ݴϴ�.
 6. �� ���ӿ��� Player�� �ι� �����Ҽ� �����Ƿ� Jump�� �ٴڿ��� ������ �ִٴ� ���¸� ǥ���ϱ� ���� Grounded�� False�� �������ݴϴ�.

  <img src="Animator.PNG" width=900 height=300>

  - �� �׸����� Entry�� ���� ���°� �����ϴ� �Ա�, Exit�� ������Ʈ ������ ����Ǵ� �ⱸ, Any State�� ������¿� ������� ����� ���·� �����ϰ� ����ϴ� ���Դϴ�.


Step4.

Player ��ũ��Ʈ ����.

```C#
using UnityEngine;

// PlayerController�� �÷��̾� ĳ���ͷμ� Player ���� ������Ʈ�� �����Ѵ�.
public class PlayerController : MonoBehaviour
{
    public AudioClip deathClip; // ����� ����� ����� Ŭ��
    public float jumpForce = 700f; // ���� ��

    private int jumpCount = 0; // ���� ���� Ƚ��
    private bool isGrounded = false; // �ٴڿ� ��Ҵ��� ��Ÿ��
    private bool isDead = false; // ��� ����

    private Rigidbody2D playerRigidbody; // ����� ������ٵ� ������Ʈ
    private Animator animator; // ����� �ִϸ����� ������Ʈ
    private AudioSource playerAudio; // ����� ����� �ҽ� ������Ʈ

    private void Start()
    {
        // �ʱ�ȭ
        playerRigidbody = GetComponent<Rigidbody2D>();
        animator = GetComponent<Animator>();
        playerAudio = GetComponent<AudioSource>();
    }

    private void Update()
    {
        // ����� �Է��� �����ϰ� �����ϴ� ó��
        if (isDead)
        {
            return;
        }
        if (Input.GetMouseButtonDown(0) && jumpCount < 2)
        {
            jumpCount++;
            playerRigidbody.velocity = Vector2.zero;
            playerRigidbody.AddForce(new Vector2(0, jumpForce));
            playerAudio.Play();
        }
        else if (Input.GetMouseButtonUp(0) && playerRigidbody.velocity.y > 0)
        {
            playerRigidbody.velocity = playerRigidbody.velocity * 0.5f;
        }
        animator.SetBool("Grounded", isGrounded);
    }

    private void Die()
    {
        // ��� ó��
        animator.SetTrigger("Die");

        playerAudio.clip = deathClip;
        playerAudio.Play();
        playerRigidbody.velocity = Vector2.zero;
        isDead = true;
    }

    private void OnTriggerEnter2D(Collider2D other)
    {
        // Ʈ���� �ݶ��̴��� ���� ��ֹ����� �浹�� ����
        if (other.tag == "Dead" && !isDead)
        {
            Die();
        }
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        // �ٴڿ� ������� �����ϴ� ó��
        if (collision.contacts[0].normal.y > 0.7f)
        {
            isGrounded = true;
            jumpCount = 0;
        }
    }

    private void OnCollisionExit2D(Collision2D collision)
    {
        // �ٴڿ��� ������� �����ϴ� ó��
        isGrounded = false;
    }
}

```

 - �ش� Player ��ũ��Ʈ�� ���� ������ Hirerachyâ�� �ִ� Player�� ��ũ��Ʈ�� ������ �ְ� �ش� ��ũ��Ʈ�� �Ҵ��ϴ� ������� ������ ������ �ָ� Player ������ ���� ���ϴ�.

Step5.

��� �����ϱ�

 - �̸� �޾Ƶ� Sky�� ���ȭ���� �����մϴ�.
 - Projectâ�� �ִ� Sky ��������Ʈ�� Hirerachyâ���� �巡���Ͽ� ����� �������ݴϴ�.
 - Main camera���� ���� ���ȭ���̶� ��︮���� �׿� ������ ������ �ݴϴ�.
 - ������ Player�� �����ӿ� ���� �����ϼ� �ֵ��� ��ũ��Ʈ�� �߰��� �ݴϴ�.

```C#
using UnityEngine;

// ���� ������Ʈ�� ��� �������� �����̴� ��ũ��Ʈ
public class ScrollingObject : MonoBehaviour {
    public float speed = 10f; // �̵� �ӵ�

    private void Update() {

        transform.Translate(Vector3.left * speed * Time.deltaTime);
        // ���ȭ���� �ʴ� speed�� �ӵ��� �������� �����̵�
    }
}
```

���� ����� ������ �ʵ��� ��Ʈ��Ʈ�� Sky�� ������ �ݴϴ�

```C#
using UnityEngine;

// ���� ������ �̵��� ����� ������ ������ ���ġ�ϴ� ��ũ��Ʈ
public class BackgroundLoop : MonoBehaviour {
    private float width; // ����� ���� ����

    private void Awake() {
        BoxCollider2D backgroundCollider = GetComponent<BoxCollider2D>();
        width = backgroundCollider.size.x;
        // BoxCollider2D ������Ʈ�� Size x���� ���� ���̷� ����մϴ�.
    }

    private void Update() {
        // ���� ��ġ�� �������� �������� width �̻� �̵������� ��ġ�� ����
        if(transform.position.x <= -width)
        {
            Reposition();
        }
    }

    // ��ġ�� �����ϴ� �޼���
    private void Reposition() {
        Vector2 offset = new Vector2(width * 2f, 0);
        transform.position = (Vector2)transform.position + offset;
        // ���� ��ġ���� ���������� ���� ���� *2 ��ŭ �̵��Ѵ�.
    }
}
```

��ũ��Ʈ�� Sky�� ���� ���� ��, Sky������Ʈ�� �����Ͽ� ��ġ�� ù ����� ���̸�ŭ �����ʿ� ��ġ��Ų �� �÷����غ��� ����� ������ �ʴ°��� �� �� �ֽ��ϴ�.

 <img src="Background.PNG" width=900 height=300>



