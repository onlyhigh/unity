내용	핵심
using UnityEngine;	Unity 기능을 스크립트에서 사용할 수 있게 연결
클래스 선언	public class Collectible : MonoBehaviour
MonoBehaviour	스크립트를 GameObject 컴포넌트로 붙여 실행하게 해 줌
Start()	게임 시작 시 한 번 실행
Update()	매 프레임 반복 실행
transform.Rotate()	GameObject를 회전시키는 함수
int	정수 자료형. 예: 1, 10
float	소수점 자료형. 예: 0.5f
변수 선언	public float rotationSpeed;
public 변수	Inspector에서 직접 값 수정 가능
이번에 만든 핵심 코드
public float rotationSpeed;

void Update()
{
    transform.Rotate(0, rotationSpeed, 0);
}
rotationSpeed 값은 Inspector의 Rotation Speed에서 조절
0.5 정도면 천천히 회전
Update()가 계속 반복되므로 아이템도 계속 회전함
이름 짓는 규칙
규칙	예시	주로 쓰는 곳
PascalCase	PlayerController, Collectible	클래스명, 메서드명
camelCase	rotationSpeed, moveDirection	변수명

# 수집 아이템 기능: 코드·용어 정리

## 1. 전체 흐름

```text
Player가 아이템 Trigger 영역에 들어감
→ OnTriggerEnter 실행
→ 닿은 대상이 Player 태그인지 확인
→ 파티클 효과 생성
→ 수집 아이템 삭제
```

## 2. 완성 코드

```csharp
public float rotationSpeed;
public GameObject onCollectEffect;

void Update()
{
    transform.Rotate(0, rotationSpeed, 0);
}

private void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("Player"))
    {
        Instantiate(onCollectEffect, transform.position, transform.rotation);
        Destroy(gameObject);
    }
}
```

> `onCollectEffect`에는 Inspector에서 VFX Prefab을 연결해야 한다.

---

## 3. Trigger 감지 관련 용어

| 부분               | 뜻                                              |
| ---------------- | ---------------------------------------------- |
| Collider         | 오브젝트의 충돌 범위                                    |
| Is Trigger       | 물리적으로 막지는 않고, 닿았는지만 감지하게 만드는 설정                |
| Trigger Collider | 통과 가능하지만 진입을 감지하는 충돌 영역                        |
| Rigidbody        | 물리·충돌 처리를 위한 컴포넌트                              |
| `OnTriggerEnter` | 다른 Collider가 Trigger 영역에 들어오면 자동 실행되는 Unity 함수 |
| `Collider other` | Trigger 영역에 들어온 상대 오브젝트 정보                     |
| `other`          | 현재 아이템과 닿은 상대 오브젝트                             |
| `{ }`            | 조건이나 함수 안에서 실행할 코드 범위                          |

### Trigger 작동 조건

```text
아이템: Collider + Is Trigger 켜기
Player 또는 아이템 중 하나: Rigidbody 필요
```

---

## 4. 함수 선언 용어

```csharp
private void OnTriggerEnter(Collider other)
```

| 부분                 | 뜻                              |
| ------------------ | ------------------------------ |
| `private`          | 이 스크립트 내부에서만 쓰는 함수             |
| `void`             | 실행만 하고 결과값은 돌려주지 않음            |
| `OnTriggerEnter`   | Unity가 자동으로 호출하는 Trigger 감지 함수 |
| `(Collider other)` | Trigger에 들어온 상대 정보를 받는 매개변수    |
| 매개변수(Parameter)    | 함수가 외부 정보를 받아 쓰도록 만든 변수        |

---

## 5. 삭제 코드

```csharp
Destroy(gameObject);
```

| 코드                    | 뜻                                        |
| --------------------- | ---------------------------------------- |
| `Destroy()`           | GameObject나 Component를 씬에서 삭제하는 Unity 함수 |
| `gameObject`          | 현재 이 스크립트가 붙어 있는 GameObject              |
| `Destroy(gameObject)` | 현재 수집 아이템 자신을 삭제                         |

`gameObject`의 g는 소문자다.

---

## 6. VFX · 파티클 효과

| 용어                  | 뜻                              |
| ------------------- | ------------------------------ |
| VFX                 | 시각 효과. 연기, 반짝임, 불꽃, 폭발 등       |
| Particle System     | 많은 작은 입자를 뿌려 VFX를 만드는 Unity 기능 |
| Prefab              | 반복 생성할 수 있는 오브젝트 원본 템플릿        |
| Prefab Editing Mode | Prefab 원본을 따로 열어 확인·수정하는 모드    |
| `onCollectEffect`   | 수집할 때 생성할 파티클 Prefab을 저장하는 변수  |

```csharp
public GameObject onCollectEffect;
```

| 부분                | 뜻                      |
| ----------------- | ---------------------- |
| `public`          | Inspector에서 연결·수정 가능   |
| `GameObject`      | 씬 오브젝트나 Prefab을 담는 자료형 |
| `onCollectEffect` | 수집 효과를 저장하는 변수 이름      |

---

## 7. 파티클 생성 코드

```csharp
Instantiate(onCollectEffect, transform.position, transform.rotation);
```

| 부분                   | 뜻                          |
| -------------------- | -------------------------- |
| `Instantiate()`      | Prefab을 복제해 실행 중인 씬에 생성    |
| `onCollectEffect`    | Inspector에서 연결한 파티클 Prefab |
| `transform.position` | 현재 수집 아이템의 위치              |
| `transform.rotation` | 현재 수집 아이템의 회전값             |
| `transform`          | 현재 아이템의 위치·회전·크기 정보        |

즉:

```text
수집 아이템이 있던 위치와 방향에
On Collect Effect Prefab을 생성한다.
```

---

## 8. Player만 수집하게 하는 조건문

```csharp
if (other.CompareTag("Player"))
{
    Instantiate(onCollectEffect, transform.position, transform.rotation);
    Destroy(gameObject);
}
```

| 코드                           | 뜻                       |
| ---------------------------- | ----------------------- |
| `if`                         | 괄호 안 조건이 맞을 때만 아래 코드 실행 |
| `other.CompareTag("Player")` | 닿은 상대의 Tag가 Player인지 확인 |
| `Tag`                        | GameObject를 구분하는 이름표    |
| `"Player"`                   | Player 태그라는 글자 데이터      |
| `{ }`                        | Player일 때만 실행할 코드 범위    |

### 꼭 설정할 것

```text
Hierarchy에서 Player 선택
→ Inspector 위쪽 Tag
→ Player 선택
```

이 설정이 없으면 `CompareTag("Player")` 조건이 통과하지 않아 아이템을 먹을 수 없다.

---

## 9. 주석

```csharp
// Destroy the collectible
```

| 기호          | 뜻                  |
| ----------- | ------------------ |
| `//`        | 이 뒤 문장은 실행되지 않는 메모 |
| Comment(주석) | 코드의 목적·계획을 적는 설명   |

---

## 10. 코드 기호 기초

| 기호    | 뜻                  |
| ----- | ------------------ |
| `.`   | 오브젝트 안의 기능이나 값에 접근 |
| `()`  | 함수 실행 또는 함수에 값 전달  |
| `,`   | 여러 값을 구분           |
| `;`   | 코드 한 줄의 끝          |
| `{ }` | 실행할 코드 묶음          |
| `" "` | 글자 데이터(String)     |
| `=`   | 오른쪽 값을 왼쪽 변수에 넣음   |

예시:

```csharp
transform.Rotate(0, rotationSpeed, 0);
```

```text
현재 아이템(transform)을
Y축(rotationSpeed 값)으로
회전(Rotate)시킨다.
```

# Unity 프로그래밍에서 했던 실수 · 용어 정리

## 1. 이번에 했던 실수

### 1-1. 점프 코드를 Collectible에 넣음

점프 기능은 Player를 움직이는 기능이라서 `PlayerController.cs`에 들어가야 한다.

```csharp
public float jumpForce = 5.0f;
```

이 코드는 `Collectible.cs`가 아니라 `PlayerController.cs`에 넣는다.

| 기능              | 들어갈 스크립트         |
| --------------- | ---------------- |
| 이동, 회전, 점프      | PlayerController |
| 아이템 회전, 수집, VFX | Collectible      |
| 문 열기            | DoorOpener       |
| 낮밤 변화           | DayNightCycle    |

---

### 1-2. 변수 이름을 바꿔서 Inspector 연결이 풀림

원래:

```csharp
public GameObject onCollectEffect;
```

중간에:

```csharp
public GameObject onCollectibleEffect;
```

로 이름을 바꾸면 Unity Inspector에서 연결해 둔 VFX Prefab이 `None`으로 풀릴 수 있다.

```text
변수 이름 변경
→ Unity가 기존 연결을 못 찾음
→ On Collect Effect가 None이 됨
→ VFX가 안 나옴
```

해결:

```text
코인 선택
→ Inspector
→ Collectible 컴포넌트
→ On Collect Effect 칸에 VFX Prefab 다시 드래그
```

---

### 1-3. Player Tag가 Player가 아니었음

수집 코드는 이렇게 Player인지 확인한다.

```csharp
if (other.CompareTag("Player"))
```

Player의 Tag가 `Untagged`면 조건이 거짓이라 아이템이 사라지지 않는다.

해결:

```text
Hierarchy에서 Player 선택
→ Inspector 맨 위 Tag
→ Player 선택
```

---

### 1-4. 점프 입력을 FixedUpdate에 넣음

처음에는 스페이스바 입력을 `FixedUpdate()` 안에서 확인했다.

```csharp
Keyboard.current.spaceKey.wasPressedThisFrame
```

이런 “이번 프레임에 눌렸는지” 확인하는 입력은 `Update()`에서 받는 편이 더 안전하다.

| 함수            | 주로 하는 일             |
| ------------- | ------------------- |
| Update()      | 키 입력, UI, 일반 게임 로직  |
| FixedUpdate() | Rigidbody 이동, 물리 계산 |

점프 입력은 `Update()`, 실제 이동은 `FixedUpdate()`에 둔다.

---

### 1-5. 코드 오류 하나가 전체 스크립트를 멈출 수 있음

Unity는 Console에 빨간 오류가 있으면 다른 스크립트도 정상 실행되지 않을 수 있다.

문제가 생기면 가장 먼저:

```text
Unity Console
→ 빨간 Error가 0개인지 확인
```

---

### 1-6. 스크립트 파일명과 클래스명이 달라질 수 있음

이름은 반드시 같아야 한다.

```text
파일: PlayerController.cs
클래스: public class PlayerController
```

```text
파일: Collectible.cs
클래스: public class Collectible
```

```text
파일: DoorOpener.cs
클래스: public class DoorOpener
```

다르면 Console 오류가 나고 스크립트가 안 붙거나 실행 안 된다.

---

### 1-7. Trigger 조건을 놓칠 수 있음

`OnTriggerEnter()`가 작동하려면 기본적으로 이 조건이 필요하다.

```text
코인: Collider 있음
코인 Collider: Is Trigger 켜짐
Player 또는 코인 중 하나: Rigidbody 있음
```

현재는 Player에 Rigidbody가 있어서 조건 충족.

---

### 1-8. Door 부모가 아니라 자식을 선택할 수 있음

문 열기 스크립트는 `DoorPanel`이나 `DoorHandle`이 아니라, Animator가 붙은 부모 `Door`에 붙여야 한다.

```text
Door
 ├─ DoorPanel
 └─ DoorHandle
```

`Door` 부모 오브젝트에:

```text
Animator
DoorOpener Script
Box Collider
Is Trigger
```

가 붙어 있어야 한다.

---

### 1-9. Animator Trigger 이름은 철자까지 같아야 함

DoorOpener 코드:

```csharp
doorAnimator.SetTrigger("Door_Open");
```

Animator의 Trigger 이름도 정확히:

```text
Door_Open
```

이어야 한다.

대소문자나 `_` 하나라도 다르면 문이 안 열린다.

---

### 1-10. 코드 안에 한글 넣기

Tooltip, Debug.Log, 주석에 한글을 넣으면 환경에 따라 깨질 수 있다.

앞으로 코드 안에는 영어만 사용.

```csharp
[Tooltip("Time in seconds for one full day-night cycle.")]
public float dayDuration = 60f;
```

한국어 설명은 코드 밖에 작성.

---

# 2. 수집 기능 최종 구조

```text
Player가 코인 Trigger에 들어감
→ OnTriggerEnter 실행
→ Player Tag인지 검사
→ VFX 생성
→ 코인 삭제
```

```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
    public float rotationSpeed;
    public GameObject onCollectEffect;

    private void Update()
    {
        transform.Rotate(0, rotationSpeed, 0);
    }

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            Instantiate(onCollectEffect, transform.position, transform.rotation);
            Destroy(gameObject);
        }
    }
}
```

---

# 3. 디버깅 순서

수집 아이템이 안 먹히면 이 순서대로 확인.

```text
1. Console 빨간 오류 0개인가?
2. Player Tag가 Player인가?
3. Player에 Rigidbody가 있는가?
4. 코인에 Collider가 있는가?
5. 코인 Collider의 Is Trigger가 켜졌는가?
6. 코인에 Collectible 스크립트가 붙었는가?
7. On Collect Effect에 VFX Prefab이 연결됐는가?
8. Player가 실제로 코인 Trigger에 닿는가?
```

| 증상                    | 가장 의심할 것                          |
| --------------------- | --------------------------------- |
| 코인이 안 사라짐             | Player Tag, Is Trigger, Rigidbody |
| 코인은 사라지는데 VFX 없음      | On Collect Effect가 None           |
| 스크립트가 Inspector에 안 붙음 | 파일명과 클래스명 불일치                     |
| 모든 기능이 이상함            | Console 빨간 오류                     |
| 문이 안 열림               | Door 부모 선택, Animator Trigger 이름   |

---

# 4. 이번에 나온 핵심 용어

## 4-1. 코드 구조

| 용어                | 뜻                     |
| ----------------- | --------------------- |
| Script            | 게임 기능을 담은 C# 코드 파일    |
| Component         | GameObject에 붙는 기능 부품  |
| Class             | 코드를 하나의 기능 단위로 묶은 구조  |
| Variable          | 값을 저장하는 이름 붙은 공간      |
| Public Variable   | Inspector에서 수정 가능한 변수 |
| Private           | 해당 스크립트 내부에서만 사용      |
| Method / Function | 특정 기능을 실행하는 코드 묶음     |
| Parameter         | 함수가 외부 정보를 받기 위한 변수   |
| Comment           | 실행되지 않는 설명 메모         |
| Data Type         | 값의 종류를 정하는 규칙         |

---

## 4-2. 자료형

| 자료형        | 뜻                      | 예시              |
| ---------- | ---------------------- | --------------- |
| int        | 정수                     | `1`, `10`, `-3` |
| float      | 소수점 숫자                 | `0.5f`, `5.0f`  |
| string     | 글자 데이터                 | `"Player"`      |
| GameObject | 씬 오브젝트나 Prefab을 담는 자료형 |                 |
| Vector3    | X, Y, Z 좌표 또는 방향 값     |                 |

---

## 4-3. Unity 함수

| 코드                          | 뜻                                |
| --------------------------- | -------------------------------- |
| `Start()`                   | 게임 시작 시 한 번 실행                   |
| `Update()`                  | 매 프레임 반복 실행                      |
| `FixedUpdate()`             | 물리 처리용 일정한 시간 간격 반복              |
| `OnTriggerEnter()`          | Trigger 영역에 다른 Collider가 들어오면 실행 |
| `Destroy()`                 | GameObject를 삭제                   |
| `Instantiate()`             | Prefab을 복제해 씬에 생성                |
| `GetComponent<Rigidbody>()` | 같은 GameObject의 Rigidbody 찾기      |
| `CompareTag("Player")`      | Tag가 Player인지 확인                 |
| `transform.Rotate()`        | 오브젝트 회전                          |
| `rb.AddForce()`             | Rigidbody에 물리 힘 적용               |

---

## 4-4. 물리 · 충돌

| 용어                | 뜻                             |
| ----------------- | ----------------------------- |
| Collider          | 충돌 범위                         |
| Is Trigger        | 통과 가능하지만 닿았는지는 감지             |
| Trigger Collider  | 이벤트 감지용 Collider              |
| Rigidbody         | 중력, 충돌, 물리 이동 담당              |
| Tag               | GameObject를 구분하는 이름표          |
| Animator          | 애니메이션을 관리하고 실행하는 컴포넌트         |
| Trigger Parameter | Animator에서 특정 애니메이션을 실행시키는 신호 |

---

# 5. 코드 기호

| 기호    | 뜻                |
| ----- | ---------------- |
| `.`   | 오브젝트 안의 기능·값에 접근 |
| `()`  | 함수 실행 또는 값 전달    |
| `{ }` | 실행할 코드 범위        |
| `;`   | 코드 한 줄의 끝        |
| `,`   | 여러 값을 구분         |
| `" "` | 글자 데이터           |
| `=`   | 오른쪽 값을 왼쪽에 저장    |
| `//`  | 주석 시작            |

예시:

```csharp
Instantiate(onCollectEffect, transform.position, transform.rotation);
```

뜻:

```text
onCollectEffect Prefab을
현재 아이템 위치와 회전값으로
씬에 새로 생성한다.
```

