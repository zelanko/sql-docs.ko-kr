---
title: 독립 실행형 SSIS(SQL Server Integration Services) DevOps 도구 | Microsoft Docs
description: 독립 실행형 SSIS DevOps 도구를 사용하여 SSIS CICD를 빌드하는 방법을 알아봅니다.
ms.date: 10/16/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1d0e6b5fe9303269f5941ba11d231e1ca18def11
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92098810"
---
# <a name="standalone-sql-server-integration-service-ssis-devops-tools-preview"></a>독립 실행형 SSIS(SQL Server Integration Services) DevOps 도구(미리 보기)

독립 실행형 **SSIS DevOps 도구**는 SSIS CICD 태스크를 수행할 수 있는 일련의 실행 파일을 제공합니다. Visual Studio 또는 SSIS 런타임 설치에 대한 종속성 없이 이러한 실행 파일을 CICD 플랫폼과 쉽게 통합할 수 있습니다. 제공되는 실행 파일은 다음과 같습니다.

- SSISBuild.exe: 프로젝트 배포 모델 또는 패키지 배포 모델에서 SSIS 프로젝트를 빌드합니다.
- SSISDeploy.exe: ISPAC 파일을 SSIS 카탈로그에 배포하거나 DTSX 파일 및 해당 종속성을 파일 시스템에 배포합니다.

## <a name="installation"></a>설치

.NET Framework 4.6.2 이상이 필요합니다.

[다운로드 센터](https://aka.ms/AA9xp65)에서 최신 설치 관리자를 다운로드한 다음 마법사 또는 명령줄을 통해 설치합니다.

- 마법사를 통해 설치

.exe 파일을 두 번 클릭하여 설치하고 실행 파일 및 종속성 파일의 압축을 풀 폴더를 지정합니다.

![설치 위치](media/installation-location.png)

- 명령줄을 통해 설치

```
SSISDevOpsTools.exe /Q /C /T:<full path>
```

![설치 명령줄](media/installation-command-line.png)


## <a name="ssisbuildexe"></a>SSISBuild.exe

**구문**

```
SSISBuild.exe -project|-p:<dtproj file path> [-configuration|-c:<configuration name>] [-projectPassword|-pp:<project password>] [-stripSensitive|-ss] [-output|-o:<output path>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**매개 변수**

|매개 변수|Description|
|---------|---------|
|-project \|-p:\<dtproj file path>|빌드할 dtproj 파일의 파일 경로입니다.|
|-configuration\|-c:\<configuration name>|빌드에 사용할 프로젝트 구성의 이름입니다. 지정하지 않으면 기본적으로 dtproj 파일에 정의된 첫 번째 프로젝트 구성으로 설정됩니다.|
|-projectPassword\|-pp:\<project password>|SSIS 프로젝트 및 해당 패키지의 암호입니다. 이 인수는 SSIS 프로젝트 및 패키지의 보호 수준이 EncryptSensitiveWithPassword 또는 EncryptAllWithPassword인 경우에만 유효합니다. 패키지 배포 모델의 경우 모든 패키지에서 이 인수에 지정된 것과 동일한 암호를 공유해야 합니다.|
|-stripSensitive\|-ss|SSIS 프로젝트의 보호 수준을 DontSaveSensitve로 변환합니다. 보호 수준이 EncryptSensitiveWithPassword 또는 EncryptAllWithPassword인 경우 -projectPassword 인수를 올바르게 설정해야 합니다. 이 옵션은 프로젝트 배포 모델에만 사용할 수 있습니다.|
|-output\|-o:\<output path>|빌드 아티팩트의 출력 경로입니다. 이 인수의 값은 프로젝트 구성의 기본 출력 경로를 덮어씁니다.|
|-log\|-l:\<log level>[;\<log path>]|로그 관련 설정입니다. <li>로그 수준: 로깅 수준이 같거나 높은 로그만 로그 파일에 기록됩니다. 다음 네 가지 로깅 수준이 있습니다(낮은 수준에서 높은 수준). DIAG, INFO, WRN, ERR. 지정하지 않으면 기본 로깅 수준이 INFO로 지정됩니다. <li> 로그 경로: 로그를 유지할 파일의 경로입니다. 경로를 지정하지 않으면 로그 파일이 생성되지 않습니다.|
|-quiet\|-q|표준 출력에 로그를 표시하지 않습니다.|
|-help\|-h\|-?|이 명령줄 유틸리티에 대한 자세한 사용 정보를 표시합니다.|

**예**

- 첫 번째 정의된 프로젝트 구성을 사용하여 암호로 암호화되지 않은 dtproj를 빌드합니다.    
    ```
    SSISBuild.exe -p:"C:\projects\demo\demo.dtproj"
    ```

- "DevConfiguration" 구성을 사용하여 암호로 암호화된 dtproj를 빌드하고 빌드 아티팩트를 특정 폴더에 출력합니다.
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -o:D:\folder
    ```

- "DevConfiguration" 구성을 사용하여 암호로 암호화되고, 중요한 데이터가 스트라이프되고, 로그 수준이 DIAG인 dtproj를 빌드합니다.
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -ss -l:diag
    ```

## <a name="ssisdeployexe"></a>SSISDeploy.exe

**구문**

```
SSISDeploy.exe -source|-s:<source path> -destination|-d:<type>;<path>[;server] [-authType|-at:<auth type name>] [-connectionStringSuffix|-css:<connection string suffix>] [-projectPassword|-pp:<project password>] [-username|-u:<username>] [-password|-p:<password>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**매개 변수**

|매개 변수|Description|
|---------|---------|
|-source\|-s:\<source path>|배포할 아티팩트의 로컬 파일 경로입니다. ISPAC, DTSX, DTSX의 폴더 경로, SSISDeploymentManfiest가 허용됩니다.|
|-destination\|-d:\<type>;\<path>[;server]|원본 파일이 배포되는 SSIS 카탈로그의 대상 유형, 대상 폴더 경로 및 서버 이름입니다. 현재 다음 두 가지 대상 유형을 지원합니다. <li> *CATALOG*: 단일 또는 여러 ISPAC 파일을 지정된 SSIS 카탈로그에 배포합니다. CATALOG 대상의 경로는 다음과 같은 형식이어야 합니다. <br> /SSISDB/\<folder name>[/\<project name>] <br> <project name>(선택 사항)은 원본에서 단일 ISPAC 파일 경로를 지정하는 경우에만 유효합니다. CATALOG 대상에 대해 서버 이름을 지정해야 합니다. <li> *FILE*: 단일 또는 여러 SSISDeploymentManifest 파일에 지정된 SSIS 패키지 또는 파일을 파일 시스템의 지정된 경로에 배포합니다. FILE 대상의 경로는 다음과 같은 형식의 로컬 폴더 경로 또는 네트워크 폴더 경로일 수 있습니다. <br>\\\\\<machine name>\\\<folder name>[\\\<sub folder name>\...]|
|-authType\|-at:\<auth type name>|SQL Server에 액세스하기 위한 인증 유형입니다. CATALOG 대상에는 필수입니다. 다음과 같은 형식이 지원됩니다. <li> WIN:  Windows 인증 <li> SQL:  SQL Server 인증 <li> ADPWD:  Active Directory - 암호 <li> ADINT:  Active Directory - 통합|
|-connectionStringSuffix\|-css:\<connection string suffix> |SSIS 카탈로그에 연결하는 데 사용되는 연결 문자열의 접미사입니다.|
|-projectPassword\|-pp:\<project password> |ISPAC 또는 DTSX 파일의 암호를 해독하는 암호입니다.|
|-username\|-u:\<username>  |지정된 SSIS 카탈로그 또는 파일 시스템에 액세스하기 위한 사용자 이름입니다. 도메인 이름의 접두사는 파일 시스템 액세스에 사용할 수 있습니다.|
|-password\|-p:\<password>  |지정된 SSIS 카탈로그 또는 파일 시스템에 액세스하기 위한 암호입니다.|
|-log\|-l:\<log level>[;\<log path>] |이 유틸리티를 실행하기 위한 로그 관련 설정입니다. <li> 로그 수준: 로깅 수준이 같거나 높은 로그만 로그 파일에 기록됩니다. 다음 네 가지 로깅 수준이 있습니다(낮은 수준에서 높은 수준). DIAG, INFO, WRN, ERR. 지정하지 않으면 기본 로깅 수준이 INFO로 지정됩니다. <li> 로그 경로: 로그를 유지할 파일의 경로입니다. 경로를 지정하지 않으면 로그 파일이 생성되지 않습니다.|
|-quiet\|-q |표준 출력에 로그를 표시하지 않습니다.|
|-help\|-h\|-?  |이 명령줄 유틸리티에 대한 자세한 사용 정보를 표시합니다.|

**예**

- Windows 인증을 사용하여 암호로 암호화되지 않은 단일 ISPAC를 SSIS 카탈로그에 배포합니다.
    ```
    SSISDeploy.exe -s:D:\myfolder\demo.ispac -d:catalog;/SSISDB/destfolder;myssisserver -at:win
    ```

- SQL 인증을 사용하여 암호로 암호화된 단일 ISPAC를 SSIS 카탈로그에 배포하고 프로젝트 이름을 바꿉니다.
    ```
    SSISDeploy.exe -s:D:\myfolder\test.ispac -d:catalog;/SSISDB/folder/testproj;myssisserver -at:sql -u:sqlusername -p:sqlpassword -pp:encryptionpassword
    ```

- 단일 SSISDeploymentManifest 및 연결된 파일을 Azure 파일 공유에 배포합니다.
    ```
    SSISDeploy.exe -s:D:\myfolder\mypackage.SSISDeploymentManifest -d:file;\\myssisshare.file.core.windows.net\destfolder -u:Azure\myssisshare -p:storagekey
    ```

- DTSX 파일의 폴더를 온-프레미스 파일 시스템에 배포합니다.
    ```
    SSISDeploy.exe -s:D:\myfolder -d:file;\\myssisshare\destfolder
    ```

## <a name="release-notes"></a>릴리스 정보

### <a name="version-010-preview"></a>버전 0.1.0 미리 보기

릴리스 날짜: 2020년 10월 16일

독립 실행형 SSIS DevOps 도구의 초기 미리 보기 릴리스입니다.

## <a name="next-steps"></a>다음 단계

- [독립 실행형 SSIS DevOps 도구](https://aka.ms/AA9xp65) 얻기
- 질문이 있는 경우 [Q&A](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools&ssr=false#qna) 방문
