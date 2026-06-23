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
