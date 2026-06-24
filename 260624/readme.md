Unity Essentials에서 배운 것 정리
1. Unity 기본 구조
용어	뜻
Scene	게임의 한 공간·한 스테이지
GameObject	씬 안의 모든 물체
Component	GameObject에 붙는 기능 부품
Inspector	선택한 오브젝트의 설정 창
Hierarchy	현재 씬 오브젝트 목록
Project	파일·Prefab·Material·Script가 있는 창
Prefab	반복 사용 가능한 오브젝트 원본
Transform	위치, 회전, 크기
GameObject
+ Component 여러 개
= 게임 속 물체 하나
2. Scene 뷰 조작
W = 이동
E = 회전
R = 크기 조절
T = Rect Tool
F = 선택한 오브젝트 화면 중앙
Ctrl + D = 복제
Ctrl + S = 저장
구분	의미
Global	월드 기준 축
Local	오브젝트가 바라보는 방향 기준 축
Perspective	원근감 있는 3D 화면
Orthographic	거리 따라 크기 안 바뀌는 2D 화면
3. 3D 씬 제작

배운 것:

바닥·벽·가구 배치
Material 적용
Skybox 적용
Directional Light로 조명 만들기
Camera 위치·각도 조절
Prefab으로 반복 오브젝트 만들기
Material과 Physics Material 차이
종류	역할
Material	색, 텍스처, 광택 같은 외형
Physics Material	마찰, 반사, 튀는 정도
4. 물리와 충돌
컴포넌트	역할
Rigidbody	3D 물리, 중력, 힘
Rigidbody 2D	2D 물리
Collider	3D 충돌 범위
Collider 2D	2D 충돌 범위
Is Trigger	통과는 가능하지만 닿았는지 감지
Rigidbody + Collider
= 실제로 부딪히는 물체

Collider + Is Trigger
= 통과는 하지만 이벤트 감지
5. 오디오
요소	역할
Audio Source	소리가 나는 위치
Audio Listener	플레이어의 귀, 보통 Main Camera
Audio Clip	실제 소리 파일
2D Audio	위치와 관계없이 들림, BGM
3D Audio	거리·방향에 따라 달라짐, 환경음
BGM = 2D Audio
냉장고·물 끓는 소리·새 소리 = 3D Audio
6. C# 스크립트 기초
용어	뜻
Script	게임 기능을 만드는 C# 파일
Class	기능을 묶은 코드 구조
Variable	값을 저장하는 이름
public	Inspector에서 조절 가능
private	해당 스크립트 안에서만 사용
Method	특정 기능을 하는 코드 묶음
자주 쓴 함수
코드	역할
Start()	시작할 때 한 번 실행
Update()	매 프레임 반복
FixedUpdate()	물리 처리 반복
Destroy()	오브젝트 삭제
Instantiate()	Prefab 생성
GetComponent()	같은 오브젝트의 Component 찾기
CompareTag()	Tag 확인
transform.Rotate()	오브젝트 회전
7. 직접 만든 핵심 기능
PlayerController
WASD / 방향키 이동
회전
점프
Rigidbody로 물리 이동
Collectible
아이템 회전
Player가 Trigger에 닿으면 감지
VFX 생성
아이템 삭제
DoorOpener
Player가 문 Trigger에 들어감
→ Animator Trigger 실행
→ Door_Open 애니메이션 재생
DayNightCycle
Directional Light 회전
→ 낮과 밤처럼 보이게 만들기
8. Tag와 Trigger
if (other.CompareTag("Player"))

뜻:

Trigger에 들어온 대상이 Player일 때만 실행
중요
Player Tag가 Player가 아니면
Collectible, Door Trigger 같은 기능이 안 될 수 있음
9. 2D 개발
3D	2D
Rigidbody	Rigidbody 2D
Collider	Collider 2D
Sphere Collider	Circle Collider 2D
OnTriggerEnter	OnTriggerEnter2D
X, Y, Z축	주로 X, Y축
2D에서 배운 것
Sprite 배치
Rect Tool로 늘리기
Order in Layer로 앞뒤 순서 조절
Rigidbody 2D와 Collider 2D
가구 밀기
Mass와 Damping 조절
2D Collectible
2D UI
10. 2D 물리값
항목	뜻
Mass	높을수록 무거워서 밀기 어려움
Gravity Scale	탑다운 게임에서는 보통 0
Linear Damping	밀린 뒤 미끄러짐 감소
Angular Damping	회전 지속 감소
Mass 높음 = 무거움
Linear Damping 높음 = 빨리 멈춤
Angular Damping 높음 = 덜 빙글빙글 돎
11. Sprite와 애니메이션
용어	뜻
Sprite	2D 이미지 오브젝트
Sprite Sheet	여러 애니메이션 그림이 모인 한 장의 이미지
Slice	Sprite Sheet를 프레임별로 자르기
Frame	애니메이션 그림 한 장
.anim	프레임 재생 순서를 담은 파일
Animator	애니메이션 재생 관리
Sprite Sheet
→ Sprite Mode: Multiple
→ Sprite Editor에서 Slice
→ 프레임 여러 개 선택
→ Hierarchy로 드래그
→ Animation 생성
12. 2D 화면 표시 순서
Order in Layer 숫자가 클수록 화면 앞에 보임

예시:

Floor = 0
Rug = 5
Furniture = 10
Player = 10

Order in Layer는 충돌이 아니라 보이는 순서를 정하는 값이다.

13. UI
요소	역할
Canvas	UI 전체의 부모
TextMeshPro	화면 글자
Button	클릭 가능한 UI
EventSystem	버튼 클릭 같은 UI 입력 처리

만든 것:

남은 Collectible 개수 표시
Main Menu
씬 선택 버튼
이름 표시
14. 씬 연결과 빌드
용어	뜻
Build	Unity 프로젝트를 실행 가능한 형태로 만드는 과정
Build Profiles	플랫폼과 빌드 설정 창
Scene List	빌드에 포함할 씬 목록
Build Index	씬의 번호
WebGL	브라우저에서 실행되는 Unity 게임

중요:

Build Index 0 = Main Menu
Build Index 1부터 = 메뉴 버튼으로 이동할 씬
15. WebGL 배포
Build Profiles
→ Web 선택
→ Switch Platform
→ Build
→ 결과 폴더 zip 압축
→ Unity Play 업로드

WebGL로 올리면 설치 없이 링크만 눌러 게임을 실행할 수 있다.

16. 자주 했던 실수
문제	먼저 확인할 것
Collectible이 안 먹힘	Player Tag가 Player인지
VFX가 안 나옴	Inspector 변수에 Prefab이 연결됐는지
Trigger가 안 됨	Collider, Is Trigger, Rigidbody
스크립트가 안 붙음	파일명과 클래스명이 같은지
문이 안 열림	Door 부모에 Animator와 Trigger가 있는지
2D 물체가 떨어짐	Gravity Scale이 0인지
가구가 너무 미끄러움	Linear Damping
가구가 너무 회전함	Angular Damping
모든 기능이 이상함	Console 빨간 Error부터 확인
메뉴 버튼이 안 됨	Build Profiles의 Scene List 순서 확인
