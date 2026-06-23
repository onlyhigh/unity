# Unity Essentials 압축 정리

## 목차

1. 꼭 외울 핵심
2. 기본 조작 · 좌표 · 탱그램
3. 3D 오브젝트 · 물리 · Prefab
4. 그림 · 카메라 · 조명
5. 오디오
6. 플레이어 이동 스크립트
7. 회전하는 수집 아이템
8. 아이템 수집 · 파티클 효과
9. 단어 모음
10. 자주 막히는 부분

---

# 1. 꼭 외울 핵심

```text
Transform = 위치 · 회전 · 크기
Mesh Filter = 모양
Mesh Renderer = 보이는 모습
Collider = 부딪히는 범위
Rigidbody = 물리적으로 움직임

Audio Source = 소리 나는 곳
Audio Listener = 듣는 귀
BGM = 2D
공간 안 물체 소리 = 3D

Script = 기능 코드
Component = GameObject에 붙는 기능 부품
```

| 기능             | 단축키 / 핵심        |
| -------------- | --------------- |
| 저장             | `Ctrl + S`      |
| Play 모드 종료     | Stop 버튼         |
| 선택한 물체 보기      | `F`             |
| 이동 / 회전 / 크기   | `W / E / R`     |
| 오브젝트 주위를 돌며 보기 | `Alt + 좌클릭 드래그` |
| 복제             | `Ctrl + D`      |
| 이름 변경          | `F2`            |

* Play 모드에서 바꾼 값은 Stop하면 원래대로 돌아감.
* 마음에 든 Play 모드 값은 Stop 후 다시 넣고 저장해야 함.

---

# 2. 기본 조작 · 좌표 · 탱그램

## 2-1. Scene 뷰 조작

| 기능        | 조작              |
| --------- | --------------- |
| 자유 이동     | 우클릭 + `WASD`    |
| 아래 / 위 이동 | `Q / E`         |
| 선택한 물체 보기 | `F`             |
| 주변을 돌며 보기 | `Alt + 좌클릭 드래그` |
| 확대 / 축소   | 마우스 휠           |
| 이동 도구     | `W`             |
| 회전 도구     | `E`             |
| 크기 도구     | `R`             |

## 2-2. Global / Local 좌표

| 구분     | 뜻                             |
| ------ | ----------------------------- |
| Global | 월드 기준 축. 오브젝트가 돌아가도 축 방향은 동일  |
| Local  | 오브젝트 기준 축. 오브젝트를 돌리면 축도 같이 회전 |

## 2-3. 탱그램 벽화

1. `Mural` 선택 → Inspector 체크박스로 활성화
2. `Mural` 더블클릭 → Gizmo에서 Top 뷰
3. 조각 선택 → `W`로 위치 조정
4. `E`로 회전
5. 다시 `W`로 미세 조정
6. `Tangram_Reference` 체크 해제 → 참고 이미지 숨김
7. `Alt + 좌클릭`으로 완성 모습 확인
8. `Ctrl + S` 저장

| 기능       | 방법                         |
| -------- | -------------------------- |
| 축 이동     | 빨강 X / 초록 Y / 파랑 Z 화살표 드래그 |
| 바닥 평면 이동 | X·Z축 사이 작은 사각형 드래그         |
| 바닥 위 회전  | 초록색 Y축 링                   |
| 원근 없는 배치 | Gizmo 우클릭 → Perspective 끄기 |
| 일반 3D 시점 | Gizmo 우클릭 → Perspective 켜기 |

---

# 3. 3D 오브젝트 · 물리 · Prefab

## 3-1. 방 만들기

* Prefab을 Project 창에서 Scene 뷰로 드래그
* 방 Position은 보통 `0, 0, 0`
* 침대·가구를 방 안에 배치
* 나중에 블록 탑이나 게임 요소를 둘 공간은 비워 두기

## 3-2. 튀는 공

| 항목          | 설정                                |
| ----------- | --------------------------------- |
| 생성          | `3D Object > Sphere`              |
| 이름          | `Ball`                            |
| Scale       | `0.25, 0.25, 0.25`                |
| Position 예시 | `2, 3, -1`                        |
| 색·광택        | `Ball_Mat`                        |
| 물리          | Rigidbody 추가                      |
| 튀는 정도       | Physics Material → Bounciness `1` |

## 3-3. Ramp · Cone · Cylinder

* 복잡한 모양은 `Mesh Collider` 사용
* Rigidbody가 붙은 Mesh Collider는 보통 `Convex` 켜기
* Collider가 있어야 공이 통과하지 않고 충돌함
* 편집 중 오브젝트를 표면 위에 맞춰 배치할 때도 Collider가 도움이 됨

## 3-4. 블록 탑

1. Cube 생성 → 이름 `Block`
2. Transform `Reset`
3. Rigidbody 추가
4. Block을 Project 창으로 드래그 → Prefab 생성
5. 여러 개 복제해 탑 만들기
6. 전부 선택 → `Create Empty Parent`
7. 부모 이름 `Block_Tower`

| 개념              | 뜻                   |
| --------------- | ------------------- |
| Prefab          | 반복해서 쓰는 오브젝트 원본 템플릿 |
| Prefab Instance | 씬 안에 배치된 복사본        |
| Prefab 원본 수정    | 연결된 모든 복사본에 적용      |
| Block Mass      | `0.1` 정도면 가벼운 블록    |
| Ball Mass       | 높이면 블록 탑을 더 잘 밀어냄   |

---

# 4. 그림 · 카메라 · 조명

## 4-1. 벽에 그림 걸기

### 가장 중요

```text
John_Lemon 이미지(Texture)
→ Art_Mat의 Base Map
→ Quad의 Material
```

* Mesh Renderer의 Material 선택창에는 **Material만** 뜸.
* John_Lemon 같은 이미지는 Texture라서 Material 목록에 안 뜨는 것이 정상.
* `Art_Mat` 선택
* Inspector → `Surface Inputs > Base Map`
* Base Map의 텍스처 칸에 John_Lemon 넣기
* 그림이 안 보이면 Quad를 Y축 `180°` 회전해 보기

### 액자 만들기

1. Quad 복제: `Ctrl + D`
2. 이름: `Frame`
3. Frame을 원래 Quad의 자식으로 만들기
4. Scale: `1.1`
5. 그림보다 약간 뒤로 이동
6. 액자용 Material 적용

## 4-2. 카메라

| 기능                      | 방법                            |
| ----------------------- | ----------------------------- |
| 현재 Scene 뷰 시점으로 카메라 맞추기 | `Ctrl + Shift + F`            |
| 카메라 시야 넓이               | Camera → Field of View        |
| Player를 따라오는 카메라        | Main Camera를 Player의 자식으로 만들기 |
| 카메라 시작 위치 예시            | Position `0, 2, -4`           |

```text
Player
 └─ Main Camera
```

## 4-3. 조명 · 하늘

| 기능        | 방법                                   |
| --------- | ------------------------------------ |
| 태양 방향     | Directional Light 회전                 |
| 밤 분위기     | Directional Light Intensity 낮추기      |
| 하늘 배경     | Skybox Material을 Scene 뷰 하늘로 드래그     |
| 하늘 적용     | Lighting → Generate Lighting         |
| Play 모드 색 | Preferences → Colors → Playmode Tint |

---

# 5. 오디오

## 5-1. 핵심 구조

```text
Audio Source = 소리 나는 곳
Audio Listener = 듣는 귀
Audio Generator / Audio Clip = 실제 소리 파일
```

예시:

```text
Boiling_Pot
→ Audio Source
→ Bubbling_Water
→ Main Camera의 Audio Listener가 들음
```

## 5-2. 2D / 3D 차이

| 구분            | 2D Audio    | 3D Audio      |
| ------------- | ----------- | ------------- |
| Spatial Blend | `0`         | `1`           |
| 거리 영향         | 없음          | 멀수록 작아짐       |
| 방향감           | 거의 없음       | 좌우 방향감 있음     |
| 사용 예시         | BGM, UI 효과음 | 냄비, 새, 냉장고, 문 |

```text
BGM = 2D
공간 안 물체 소리 = 3D
```

## 5-3. 주방 씬 설정

| 오브젝트             | 소리             | Loop | Spatial Blend | 핵심                 |
| ---------------- | -------------- | ---: | ------------: | ------------------ |
| Boiling_Pot      | Bubbling_Water |   켜기 |             1 | 가까우면 크게 들림         |
| Background Music | 음악             |   켜기 |             0 | Volume `0.1 ~ 0.5` |
| Bird_1           | SFX_Bird_1     | 보통 끔 |             1 | 랜덤 재생              |
| Bird_2 / Bird_3  | 다른 새소리         | 보통 끔 |             1 | 외부 여러 곳 배치         |
| Refrigerator     | Fridge-Hum     |   켜기 |             1 | Volume 낮게          |

## 5-4. 거리 설정

| 설정            | 뜻                  |
| ------------- | ------------------ |
| Volume        | 전체 기본 소리 크기        |
| Loop          | 끝나면 반복 재생          |
| Play On Awake | 시작하자마자 재생          |
| Min Distance  | 이 거리 안에서는 가장 크게 들림 |
| Max Distance  | 이 거리 근처부터 거의 안 들림  |

## 5-5. 효과 구분

| 기능          | 담당                |
| ----------- | ----------------- |
| 김, 불꽃, 거품   | Particle System   |
| 끓는 물 소리     | Audio Source      |
| 플레이어 귀      | Audio Listener    |
| 거리 따라 볼륨 변화 | Spatial Blend 3D  |
| 실내 울림       | Audio Reverb Zone |

---

# 6. 플레이어 이동 스크립트

## 6-1. 설정 순서

1. `Edit > Project Settings > Player`
2. Other Settings → Active Input Handling
3. `Input System Package (New)` 선택
4. Unity 재시작
5. `4_LivingRoom_Programming_Scene` 열기
6. 캐릭터 배치 → 이름 `Player`
7. Scripts 폴더에서 `PlayerController` 생성
8. PlayerController를 Player에 드래그
9. 스크립트 더블클릭 → Visual Studio 열기
10. 코드 붙여넣기 → `Ctrl + S`
11. Main Camera를 Player의 자식으로 만들기
12. Play 모드에서 속도 조절 후, Play 모드 밖에서 다시 저장

## 6-2. Player 구조

```text
Player
 ├─ Rigidbody
 ├─ PlayerController
 └─ Main Camera
```

| 요소               | 역할          |
| ---------------- | ----------- |
| Rigidbody        | 물리 방식 이동    |
| PlayerController | 키보드 입력 처리   |
| Main Camera      | Player를 따라감 |

## 6-3. 조작

| 키         | 동작     |
| --------- | ------ |
| `W` / `↑` | 앞으로    |
| `S` / `↓` | 뒤로     |
| `A` / `←` | 왼쪽 회전  |
| `D` / `→` | 오른쪽 회전 |

## 6-4. Inspector에서 바꾸는 값

```csharp
public float speed = 5.0f;
public float rotationSpeed = 120.0f;
```

| 항목             | 뜻        |
| -------------- | -------- |
| Speed          | 앞뒤 이동 속도 |
| Rotation Speed | 좌우 회전 속도 |

* `public` 변수는 Inspector에서 수정 가능
* Play 모드에서 테스트한 값은 Stop하면 돌아감
* PlayerController가 작동하려면 Player에 Rigidbody 필요
* PlayerController 파일명과 코드 클래스명은 같아야 함

```text
파일: PlayerController.cs
클래스: public class PlayerController
```

---

# 7. 회전하는 수집 아이템

## 7-1. Collectible 스크립트 만들기

1. Scripts 폴더 빈 곳 우클릭
2. `Create > MonoBehaviour Script`
3. 이름: `Collectible`
4. 수집 아이템 GameObject에 붙이기

## 7-2. 기본 스크립트 구조

```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
    void Start()
    {
    }

    void Update()
    {
    }
}
```

| 코드                                         | 뜻                                      |
| ------------------------------------------ | -------------------------------------- |
| `using UnityEngine;`                       | Unity 기능을 이 스크립트에서 사용할 수 있게 연결         |
| `public class Collectible : MonoBehaviour` | Collectible이라는 Unity 컴포넌트 스크립트 선언      |
| `Start()`                                  | 게임 시작할 때 한 번 실행                        |
| `Update()`                                 | 매 프레임 반복 실행                            |
| `MonoBehaviour`                            | 스크립트를 GameObject에 Component로 붙여 실행하게 함 |

## 7-3. 회전 코드

```csharp
public float rotationSpeed;

void Update()
{
    transform.Rotate(0, rotationSpeed, 0);
}
```

| 코드              | 뜻                        |
| --------------- | ------------------------ |
| `transform`     | 이 스크립트가 붙은 아이템의 위치·회전·크기 |
| `Rotate()`      | 오브젝트를 회전시키는 Unity 함수     |
| 첫 번째 `0`        | X축 회전 없음                 |
| `rotationSpeed` | Y축 회전 속도                 |
| 마지막 `0`         | Z축 회전 없음                 |

* Inspector의 `Rotation Speed`에 `0.5` 정도를 넣으면 천천히 회전.
* `Update()`가 계속 반복돼서 아이템도 계속 회전.

## 7-4. 숫자 자료형

| 자료형    | 뜻            | 예시              |
| ------ | ------------ | --------------- |
| int    | 정수           | `1`, `10`, `-3` |
| float  | 소수점 숫자       | `0.5f`, `2.0f`  |
| double | 더 정밀한 소수점 숫자 | `0.5`           |

```csharp
transform.Rotate(0, 0.5f, 0);
```

* C#에서 소수점 값을 float로 쓸 때는 보통 뒤에 `f`를 붙임.
* `0.5` 대신 `0.5f` 사용.

## 7-5. 이름 규칙

| 규칙         | 예시                                | 주로 쓰는 곳    |
| ---------- | --------------------------------- | ---------- |
| PascalCase | `PlayerController`, `Collectible` | 클래스명, 메서드명 |
| camelCase  | `rotationSpeed`, `moveDirection`  | 변수명        |

---

# 8. 아이템 수집 · 파티클 효과

## 8-1. 전체 흐름

```text
Player가 아이템 Trigger 영역에 들어감
→ OnTriggerEnter 실행
→ 닿은 대상이 Player 태그인지 확인
→ 파티클 효과 생성
→ 수집 아이템 삭제
```

## 8-2. Trigger 설정

수집 아이템의 Collider에서 **Is Trigger** 체크를 켭니다.

```text
일반 Collider = 물리적으로 막음
Is Trigger = 통과는 가능, 닿았는지는 감지
```

### Trigger 작동 조건

```text
아이템: Collider + Is Trigger 켜기
Player 또는 아이템 중 하나: Rigidbody 필요
```

Player에 Rigidbody가 있으므로 튜토리얼에서는 조건 충족.

## 8-3. 수집 효과 연결

```csharp
public GameObject onCollectEffect;
```

| 부분                | 뜻                       |
| ----------------- | ----------------------- |
| `public`          | Inspector에서 연결·수정 가능    |
| `GameObject`      | 씬 오브젝트나 Prefab을 담는 자료형  |
| `onCollectEffect` | 수집할 때 생성할 파티클 Prefab 변수 |

* Inspector의 `On Collect Effect` 칸에 VFX Prefab을 드래그해서 연결.
* 연결하지 않으면 파티클이 생성되지 않음.

## 8-4. 최종 Collectible 코드

```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
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
}
```

## 8-5. Trigger 감지 함수

```csharp
private void OnTriggerEnter(Collider other)
```

| 부분               | 뜻                                |
| ---------------- | -------------------------------- |
| `private`        | 이 스크립트 내부에서만 쓰는 함수               |
| `void`           | 실행만 하고 결과값은 돌려주지 않음              |
| `OnTriggerEnter` | Trigger에 다른 Collider가 들어오면 자동 실행 |
| `Collider other` | Trigger에 들어온 상대 오브젝트 정보          |
| 매개변수(Parameter)  | 함수가 외부 정보를 받아 쓰도록 만든 변수          |

## 8-6. Player만 수집하게 제한

```csharp
if (other.CompareTag("Player"))
{
    Instantiate(onCollectEffect, transform.position, transform.rotation);
    Destroy(gameObject);
}
```

| 코드                     | 뜻                     |
| ---------------------- | --------------------- |
| `if`                   | 조건이 맞을 때만 아래 코드 실행    |
| `other`                | 이 아이템 Trigger에 들어온 상대 |
| `CompareTag("Player")` | 상대의 Tag가 Player인지 확인  |
| `"Player"`             | Player라는 글자 데이터       |
| `{ }`                  | 조건이 맞을 때 실행할 코드 묶음    |

### Player Tag 설정

```text
Hierarchy에서 Player 선택
→ Inspector 위쪽 Tag
→ Player 선택
```

Player Tag가 없으면 아이템을 먹을 수 없음.

## 8-7. 파티클 생성

```csharp
Instantiate(onCollectEffect, transform.position, transform.rotation);
```

| 부분                   | 뜻                          |
| -------------------- | -------------------------- |
| `Instantiate()`      | Prefab을 복제해 실행 중인 씬에 생성    |
| `onCollectEffect`    | Inspector에서 연결한 파티클 Prefab |
| `transform.position` | 현재 수집 아이템 위치               |
| `transform.rotation` | 현재 수집 아이템 회전값              |

뜻:

```text
수집 아이템이 있던 위치와 방향에
On Collect Effect Prefab을 생성한다.
```

## 8-8. 아이템 삭제

```csharp
Destroy(gameObject);
```

| 코드                    | 뜻                             |
| --------------------- | ----------------------------- |
| `Destroy()`           | GameObject나 Component를 씬에서 삭제 |
| `gameObject`          | 이 스크립트가 붙은 현재 GameObject      |
| `Destroy(gameObject)` | 현재 수집 아이템 자신을 삭제              |

* `gameObject`의 g는 소문자.

## 8-9. 아이템 길 만들기 · Hierarchy 정리

| 기능     | 방법                              |
| ------ | ------------------------------- |
| 복제     | `Ctrl + D`                      |
| 일직선 배치 | Global 좌표 + X/Y/Z 화살표           |
| 일정한 간격 | `Ctrl` 누른 채 이동                  |
| 위에서 배치 | Top 뷰                           |
| 묶기     | 여러 아이템 선택 → Create Empty Parent |
| 부모 이름  | `Collectibles`                  |

```text
Collectibles
 ├─ Collectible
 ├─ Collectible (1)
 ├─ Collectible (2)
 └─ Collectible (3)
```

---

# 9. 단어 모음

## 9-1. 3D · 물리

| 용어               | 뜻                             |
| ---------------- | ----------------------------- |
| Transform        | 위치, 회전, 크기                    |
| Mesh Filter      | 3D 모양 데이터                     |
| Mesh Renderer    | 모양을 화면에 보이게 함                 |
| Sphere Collider  | 구 형태 충돌 범위                    |
| Mesh Collider    | 실제 Mesh 모양을 따라가는 충돌 범위        |
| Convex           | Mesh Collider를 단순한 볼록 충돌체로 만듦 |
| Rigidbody        | 중력, 충돌, 물리 이동                 |
| Material         | 색, 광택, 텍스처 등 보이는 모습           |
| Physics Material | 마찰력, 튀는 정도 같은 물리 성질           |
| Prefab           | 재사용 가능한 원본 템플릿                |

## 9-2. 오디오 · VFX

| 용어              | 뜻                        |
| --------------- | ------------------------ |
| Audio Source    | 소리가 발생하는 곳               |
| Audio Listener  | 소리를 듣는 귀 역할              |
| Audio Generator | 재생할 소리 파일                |
| Spatial Blend   | 2D와 3D 비율                |
| Particle System | 김, 불꽃, 거품 같은 시각 효과       |
| VFX             | 연기, 반짝임, 불꽃, 폭발 같은 시각 효과 |
| Reverb Zone     | 공간의 울림을 만드는 오디오 영역       |
| CC0             | 상업적 사용까지 비교적 자유로운 자료     |
| CC BY-NC        | 출처 표기 필요, 상업적 사용 금지      |

## 9-3. 코딩

| 용어                   | 뜻                                 |
| -------------------- | --------------------------------- |
| C#                   | Unity 게임 기능을 만드는 언어               |
| Script               | 기능을 담은 코드 파일                      |
| MonoBehaviour Script | GameObject에 붙일 수 있는 Unity 기본 스크립트 |
| Component            | GameObject에 붙는 기능 부품              |
| Script Editor        | C# 코드를 작성하는 프로그램                  |
| IDE                  | 코딩, 오류 확인, 프로젝트 관리를 돕는 프로그램       |
| Visual Studio        | Unity C# 개발에 자주 쓰는 IDE            |
| Start()              | 게임 시작 때 한 번 실행                    |
| Update()             | 매 프레임 반복 실행                       |
| FixedUpdate()        | 물리 처리용 일정 간격 반복                   |
| Input System         | 키보드·마우스·패드 입력 시스템                 |
| Keyboard.current     | 현재 키보드 입력 확인                      |
| Child GameObject     | 부모를 따라 이동·회전하는 자식 오브젝트            |
| Inspector            | 오브젝트와 Component 설정을 바꾸는 창         |
| Tag                  | GameObject를 구분하는 이름표              |
| Comment              | 코드 목적을 설명하는 메모                    |

## 9-4. 코드 기호

| 기호    | 뜻                  |
| ----- | ------------------ |
| `.`   | 오브젝트 안의 기능이나 값에 접근 |
| `()`  | 함수 실행 또는 함수에 값 전달  |
| `,`   | 여러 값을 구분           |
| `;`   | 코드 한 줄의 끝          |
| `{ }` | 실행할 코드 묶음          |
| `" "` | 글자 데이터(String)     |
| `=`   | 오른쪽 값을 왼쪽 변수에 넣음   |
| `//`  | 실행되지 않는 주석 시작      |

예시:

```csharp
transform.Rotate(0, rotationSpeed, 0);
```

```text
현재 아이템(transform)을
Y축(rotationSpeed 값)으로
회전(Rotate)시킨다.
```

---

# 10. 자주 막히는 부분

| 문제                           | 확인할 것                                |
| ---------------------------- | ------------------------------------ |
| 그림 Texture가 Material 목록에 안 뜸 | Art_Mat의 Base Map 텍스처 칸에 넣기          |
| Player가 안 움직임                | Rigidbody가 Player에 있는지 확인            |
| 키가 안 먹음                      | Game 뷰 한 번 클릭                        |
| 코드가 빨간 줄                     | 스크립트 파일명과 클래스명이 같은지 확인               |
| 카메라가 안 따라감                   | Main Camera가 Player 자식인지 확인          |
| Play 중 바꾼 값이 사라짐             | Stop 후 다시 설정하고 `Ctrl + S`            |
| 물체가 통과함                      | Collider 또는 Mesh Collider 확인         |
| 냉장고·냄비 소리가 어디서나 똑같음          | Spatial Blend를 `1`로 설정               |
| Trigger가 실행 안 됨              | Is Trigger 체크 + Rigidbody 조건 확인      |
| Player가 아이템을 못 먹음            | Player Tag가 `Player`인지 확인            |
| 파티클이 안 나옴                    | On Collect Effect에 VFX Prefab 연결 확인  |
| 아이템이 의자에 닿아 사라짐              | `if (other.CompareTag("Player"))` 확인 |
