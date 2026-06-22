Unity Editor 첫 튜토리얼 핵심 정리
1. Project 창

프로젝트 안에 있는 모든 파일을 보는 곳이야.

씬, 이미지, 모델, 스크립트, 사운드 같은 에셋 파일 전체가 들어 있음
폴더처럼 정리되어 있음
이번에는
Assets > Unity Essentials > Scenes > 1_Starter_Scene
을 더블클릭해서 씬을 열었음
2. Hierarchy 창

현재 열어 둔 씬 안에 배치된 GameObject 목록을 보는 곳이야.

현재 씬에 실제로 들어가 있는 오브젝트만 표시됨
예: Ground, Robot, Stairs, Star, Boxes
GameObject는 게임 안에 존재하는 모든 물체라고 보면 됨
예: 바닥, 캐릭터, 카메라, 조명, 계단, 아이템
부모·자식 구조

Hierarchy에서는 오브젝트가 폴더처럼 묶일 수 있음.

부모 GameObject: 다른 오브젝트를 포함하는 쪽
자식 GameObject: 부모 안에 들어 있는 오브젝트

Boxes 옆 삼각형을 누르면 안의 자식 오브젝트를 볼 수 있음.

중요한 기능

Hierarchy에서 오브젝트를 더블클릭하면 Scene 뷰가 그 오브젝트를 중심으로 이동함.

길 잃었을 때는 Ground를 더블클릭하면 전체 바닥 기준으로 다시 보기 편함.

3. Scene 뷰

게임을 만드는 사람이 씬을 편집하고 둘러보는 3D 작업 공간이야.

여기서 오브젝트를 움직이고, 회전시키고, 크기를 바꾸고, 여러 각도에서 확인함.

화면 둘러보기
마우스 오른쪽 클릭 + 드래그: 시점 회전
방향키
↑ ↓: 앞뒤 이동
← →: 좌우 이동
손 모양인 Pan 도구를 선택한 뒤
Scene 뷰에서 왼쪽 클릭 + 드래그: 화면 이동

Pan 도구와 View 도구는 사실상 씬을 둘러보는 도구라고 생각하면 돼.

4. Game 뷰와 Play 모드

Game 뷰는 실제 플레이어가 보게 되는 화면이야.

상단 중앙의 ▶ Play 버튼을 누르면 게임 테스트가 시작되고, 자동으로 Game 뷰로 전환돼.

로봇 조작
방향키 또는 WASD: 이동
Space: 점프
마우스: 시점 회전
Shift: 달리기
마우스 커서가 사라지면 Esc

테스트가 끝나면 상단의 ■ Stop 버튼으로 Play 모드를 꺼야 해.

중요한 점은 Play 모드 중에 바꾼 내용은 Stop을 누르면 저장되지 않는다는 거야.
진짜 씬 수정은 Play 모드 밖에서 해야 함.

5. Inspector 창

선택한 GameObject의 상세 설정을 보는 곳이야.

Hierarchy나 Scene 뷰에서 어떤 오브젝트를 클릭하면 Inspector에 그 오브젝트 정보가 표시됨.

여기에는 여러 Component(컴포넌트) 가 붙어 있는데, 컴포넌트는 오브젝트의 기능과 성질을 정하는 요소야.

예를 들면:

Transform: 위치, 회전, 크기
Rigidbody: 물리 움직임
Collider: 충돌 판정
Script: 직접 만든 동작 코드
Transform에서 자주 보는 것
Position: 위치
Rotation: 회전
Scale: 크기

이번 실습에서는 Star를 선택하고:

X Position을 1~2 줄여 플랫폼 쪽으로 옮기고
Y Position을 1~2 줄여 아래로 내렸음

그래서 점프로 별을 먹을 수 있게 만든 거야.

실수했으면 Ctrl + Z로 되돌리면 됨.

6. 저장

Unity는 씬을 자동 저장하지 않아.

저장: Ctrl + S
맥: Cmd + S
메뉴로는 File > Save

Hierarchy 창 위쪽 씬 이름 옆에 *가 있으면 아직 저장 안 된 상태야.

예:
1_Starter_Scene *

저장하면 별표가 사라짐.



중요 단어들
창	역할
Project	프로젝트 전체 파일 모음
Hierarchy	현재 씬 안의 GameObject 목록
Inspector	선택한 GameObject의 상세 설정
