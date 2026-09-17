# GameEngine - DirectX 11 Triangle

Rastertek의 Windows 10 / DirectX 11 튜토리얼 4 공식 배포 소스 구조에 맞춘 예제입니다.

공식 소스와 다른 부분은 프로젝트 폴더명이 `Engine`이 아니라 `GameEngine`이므로
`colorshaderclass.cpp`의 셰이더 상대 경로를 `../GameEngine/color.vs`,
`../GameEngine/color.ps`로 바꾼 것뿐입니다. 클래스 구조와 구현 방식은 공식 소스를 유지합니다.

## 실행

1. Visual Studio 2022에서 `GameEngine.sln`을 엽니다.
2. 구성을 `Debug | x64`로 선택합니다.
3. `F5` 또는 `Ctrl+F5`로 실행합니다.
4. 초록색 삼각형이 표시되며 `Esc` 키로 종료할 수 있습니다.

명령줄 빌드 예시:

```powershell
& "C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe" `
  .\GameEngine.sln /t:Build /p:Configuration=Debug /p:Platform=x64
```

## 구조와 배울 점

- `SystemClass`: Win32 창, 메시지 루프, 키 입력과 애플리케이션 수명을 관리합니다.
- `ApplicationClass`: 렌더링 객체를 조립하고 프레임 단위 렌더 순서를 관리합니다.
- `D3DClass`: Direct3D 장치, 스왑 체인, 렌더 타깃, 깊이 버퍼, 뷰포트를 생성합니다.
- `ModelClass`: 삼각형의 정점/인덱스 버퍼를 만들고 Input Assembler에 연결합니다.
- `CameraClass`: 카메라 위치와 회전으로 뷰 행렬을 계산합니다.
- `ColorShaderClass`: HLSL 셰이더를 컴파일하고 입력 레이아웃 및 행렬 상수 버퍼를 연결합니다.
- `color.vs`, `color.ps`: 월드/뷰/투영 변환과 정점 색상 출력을 담당합니다.

이 단계는 튜토리얼 원문과 동일하게 DirectX COM 객체를 원시 포인터로 보관하고
`Shutdown`에서 `Release()`하는 학습용 구조를 사용합니다.

핵심 렌더 흐름은 `화면 지우기 -> 카메라/행렬 갱신 -> 버퍼 바인딩 -> 셰이더 바인딩 -> DrawIndexed -> Present`입니다.

## 참고

- https://www.rastertek.com/tutdx11win10.html
- https://www.rastertek.com/dx11win10tut02.html
- https://www.rastertek.com/dx11win10tut03.html
- https://www.rastertek.com/dx11win10tut04.html
