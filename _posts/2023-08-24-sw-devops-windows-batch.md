---
title: (Windows-Batch) BATCH 작성 명령어
date: 2023-08-24 11:00:00:00 +0900
categories: [SW DevOps, OS]
tags: [swdevops, windows, natives, windowsbatch]     # TAG names should always be lowercase
--- 

## Windows OS Batch 예제 
전통적으로 윈도우즈OS에 프로그램을 설치할 경우, batch file을 만들어 installshield 같은<br/>
설치프로그램에서 호출하여 필요한 라이브러리를 설치함. 
python 설치 후 python library를 설치하는 과정을 windows batch 로 작성한 예제<br/>
line 9 : 온라인이 보장되는 환경에서 원격서버에서 직접 설치하는 명령어<br/>
line 10 : 온라인이 보장이 되지 않을경우, 미리 라이브러리를 다운받은 상태에서 설치하는 명령어<br/>

``` batch
@echo off
set ValueData=""
set ValueData2=""
set KEY_NAME="HKEY_CURRENT_USER\SOFTWARE\Python\PythonCore\3.10\InstallPath"
FOR /F "usebackq skip=2 tokens=3" %%P IN (`reg query %KEY_NAME% /ve`) DO ( set ValueData=%%P)
echo %ValueData%
IF NOT %ValueData%=="" set scriptpath=%ValueData%\Scripts
IF NOT %ValueData%=="" set command=%scriptpath%\pip.exe
REM IF NOT %ValueData%=="" %command% install -r "%~dp0..\wasting\requirements.txt"
IF NOT %ValueData%=="" %command% install --no-warn-script-location --no-index --find-links=%~dp0\packages\one\ -r "%~dp0..\wasting\requirements.txt"

IF %ValueData%=="" set KEY_NAME_LM="HKEY_LOCAL_MACHINE\SOFTWARE\Python\PythonCore\3.10\InstallPath"
IF %ValueData%=="" FOR /F "skip=2 tokens=3 usebackq" %%P IN (`reg query %KEY_NAME_LM% /ve`) DO ( set ValueData1=%%P)
IF %ValueData%=="" FOR /F "usebackq skip=2 tokens=4" %%P IN (`reg query %KEY_NAME_LM% /ve`) DO ( set ValueData2=%%P)
IF NOT %ValueData2%=="" GOTO PROGRAMFILES
IF %ValueData2%=="" GOTO NOPROGRAMFILES

:PROGRAMFILES
IF %ValueData%=="" set scriptpath1=%ValueData1%
IF %ValueData%=="" set scriptpath2=%ValueData2%Scripts
IF %ValueData%=="" set scriptpath3=%scriptpath1% %scriptpath2%
IF %ValueData%=="" set command="%scriptpath3%\pip.exe"
REM IF %ValueData%=="" %command% install -r "%~dp0..\wasting\requirements.txt"
IF %ValueData%=="" %command% install --no-warn-script-location --no-index --find-links=%~dp0\packages\one\ -r "%~dp0..\wasting\requirements.txt"

:NOPROGRAMFILES
IF %ValueData%=="" set scriptpath1=%ValueData1%Scripts
IF %ValueData%=="" set command="%scriptpath1%\pip.exe"
REM IF %ValueData%=="" %command% install -r "%~dp0..\wasting\requirements.txt"
IF %ValueData%=="" %command% install --no-warn-script-location --no-index --find-links=%~dp0\packages\one\ -r "%~dp0..\wasting\requirements.txt"
```

## Windows OS Batch 명령어 설명
1. ECHO - 명령실행을 복명복창 하거나 하지 않도록 함<br/>
   @echo on : 모든 명령 라인 실행결과 보여줌 (아무것도 안쓰면 echo on임)<br/>
   @echo off : 모든 명령라인 실행 결과를 막음, 만약 뭔가 보고 싶으면 echo 명령어를 활용<br/>
   @를 붙여주는 이유는 자기 자신에 대한 echo 효과를 막기위함.<br/>
2. REM - 주석
3. PAUSE - 처리를 잠시 멈추고 조건적인 메시지를 보여줌. 사용자가 어떤 키를 누르면 계속 처리진행
   PAUSE [message]
4. SET 
5. IF
6. FOR
7. GOTO
8. =
9. ==
10. CALL - 또 다른 배치파일 실행시킴