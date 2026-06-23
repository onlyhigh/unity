1-4.탱그램 벽화 만들기 핵심 정리
Mural GameObject를 Hierarchy에서 선택하고 Inspector 체크박스로 활성화
Mural 더블클릭 후 Gizmo의 Top 뷰로 위에서 내려다보기
Move 도구: W
Rotate 도구: E
개념/기능	내용·조작
Global 좌표	월드 기준, 모든 오브젝트의 축 방향이 동일
Local 좌표	오브젝트 회전 방향에 따라 축도 같이 회전
조각 이동	Move 도구에서 X(빨강), Y(초록), Z(파랑) 축 화살표 드래그
바닥에서 이동	X·Z축 사이 작은 보라색 사각형 드래그
조각 회전	Rotate 도구의 색깔 링 드래그
바닥 위 조각 회전	초록색 Y축 링 사용
추천 작업 순서	조각 선택 → W로 위치 조정 → E로 회전 → 다시 W로 미세 조정
Isometric 모드	Gizmo 우클릭 → Perspective 끄기, 원근감 없이 배치
Perspective 모드	Gizmo 우클릭 → Perspective 켜기, 자연스러운 3D 화면
참고 이미지 숨기기	Tangram_Reference 선택 → Inspector 체크박스 끄기
완성 확인	Alt + 좌클릭 드래그로 Orbit 하며 보기
저장	Ctrl + S

1-5 Editor Essentials: 선택 도전 과제 정리
1. Easy — Q, E로 링 코스 통과
기능	조작
링 다시 켜기	Rings 선택 → Inspector 체크박스 켜기
자유 비행	우클릭 누른 채 WASD
아래로 이동	Q
위로 이동	E
너무 빠를 때	Scene 뷰 Camera Speed 낮추기
2. Medium — 벽화 하나 더 만들기
기능	조작
기존 조각 전체 선택	Mural > Puzzle_Pieces 선택
조각 세트 복사	Ctrl + D
이동 도구	W
회전 도구	E
참고 이미지 켜기	Tangram_Reference 체크박스 켜기
평면 이동	X·Z축 사이 작은 사각형 드래그
3. Expert — 튜브 미끄럼틀 조립
기능	조작
미끄럼틀 켜기	Tube_Slide 선택 → 체크박스 켜기
추천 좌표	Local 좌표 사용
똑바른 방향 확인	초록색 Local Y축이 위를 향함
높이 맞추기	다리가 바닥에 닿게 조절
완성 후 전체 이동	부모 Tube_Slide 선택 후 이동·회전
마지막
선택 과제는 안 해도 됨.
Unity Learn에서 Complete Mission 1 → Mark All Steps Complete
Done을 누르고 다음 Mission으로 진행.

새 용어 정리
용어	Unity에서 뜻
Mesh Filter	오브젝트의 3D 모양 데이터를 담음. Sphere, Cube, Cone 같은 형태를 결정함
Mesh Renderer	Mesh Filter의 모양을 화면에 보이게 렌더링함. Material, 색, 텍스처, 그림자 설정이 여기 들어감
Sphere Collider	구 모양의 충돌 범위. Ball이 바닥·Ramp·블록에 부딪히게 해 줌
Mesh Collider	Mesh의 실제 모양을 따라가는 충돌 범위. Cone, Cylinder, Ramp처럼 단순한 Collider로 맞추기 어려운 모양에 사용
Convex	Mesh Collider를 빈틈·굴곡이 없는 볼록한 충돌체로 단순화하는 옵션. Rigidbody가 붙은 Mesh Collider는 보통 Convex를 켜야 물리 충돌 가능
Rigidbody	중력, 질량, 충돌 후 움직임 같은 물리 효과를 적용함
Material	물체의 보이는 모습: 색, 금속 느낌, 매끈함, 이미지 텍스처
Physics Material	물체의 물리 성질: 튀는 정도(Bounciness), 마찰력 등
제일 중요하게 구분하기

Mesh Filter = 모양
Mesh Renderer = 보이는 모습
Collider = 부딪히는 범위
Rigidbody = 물리적으로 움직임

지금까지 공부한 Unity 핵심 정리
1. 방 만들기
Prefab을 Project 창에서 Scene 뷰로 드래그해 방·침대·가구 추가
Transform에서 Position / Rotation / Scale 조절
방은 Position 0, 0, 0 원점에 배치
W 이동 / E 회전 / R 크기 조절
나중에 블록 탑을 둘 방 한쪽은 비워 두기
2. 튀는 공 만들기
3D Object > Sphere 추가 → 이름 Ball
Scale 0.25, 0.25, 0.25
Position X=2, Y=3, Z=-1
Ball_Mat으로 색·광택 설정
Rigidbody 추가 → 중력 적용
Ball_Physics 생성 → Bounciness 1
Ramp에는 Mesh Collider + Convex 추가해서 공이 통과하지 않게 함
3. 블록 탑 만들기
Cube 추가 → Block으로 이름 변경
Transform Reset으로 원점 초기화
Block에 Rigidbody 추가
Block을 Project 창으로 드래그해 Prefab 생성
Block Prefab 여러 개를 쌓아 탑 만들기
Block들을 Create Empty Parent로 묶고 부모 이름을 Block_Tower로 설정
Block Prefab 원본을 수정하면 모든 Block 인스턴스에 적용됨
Block 질량은 0.1, Ball 질량은 더 높이면 탑을 잘 쓰러뜨림
4. 다른 도형 추가
Cone, Cylinder 같은 도형도 Mesh Collider + Convex + Rigidbody를 붙이면 물리 충돌 가능
편집 중 표면 감지·배치 기능을 쓰려면 Collider가 필요할 수 있음
Cone이나 Cylinder는 서로 겹치지 않게 올리고 싶으면 Collider를 먼저 붙이고 위치를 맞추기
5. 그림 걸기

중요한 흐름:

John_Lemon 이미지(Texture) → Art_Mat의 Base Map → Quad의 Material

Mesh Renderer의 Material 선택창에는 Material만 보여서 John_Lemon 이미지가 검색 안 되는 것이 정상
Art_Mat 선택 → Inspector → Surface Inputs > Base Map의 텍스처 칸에 이미지 넣기
Quad는 한쪽 면만 보이므로 그림이 안 보이면 Y축으로 180° 돌려 보기
Quad 복제 → Frame으로 이름 변경 → Scale 1.1 → 뒤로 조금 이동 → 액자용 Material 적용
6. 카메라·조명·배경
기능	조작
카메라 현재 Scene 뷰 시점으로 맞추기	Ctrl + Shift + F
카메라 이동 / 회전	W / E
화면 넓이	Camera → Field of View
태양 방향	Directional Light 회전
하늘 배경	Skybox를 Scene 뷰 하늘로 드래그
새 하늘 반영	Lighting → Generate Lighting
Play 모드 색 변경	Preferences → Colors → Playmode Tint
꼭 기억
Play 모드 중 수정은 Stop하면 사라짐
저장은 Ctrl + S
F는 선택한 물체를 화면 중앙에 맞춤
Alt + 좌클릭 드래그는 오브젝트 주위를 회전하며 보기
