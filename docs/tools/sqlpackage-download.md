---
title: 다운로드 및 설치 sqlpackage | Microsoft Docs
description: 다운로드 하 여 Windows, macOS 등 또는 Linux 용 sqlpackage 설치
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 4e5528ca046de83385171890fbda389928e41cf3
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703853"
---
# <a name="download-and-install-sqlpackage"></a>다운로드 해 서 sqlpackage를 설치 합니다.

sqlpackage 창, macOS 등 및 Linux에서 실행 됩니다.

다운로드 및 설치 하 고 최신.NET Framework 릴리스 및 macOS Linux 미리 보기:

|플랫폼|다운로드|릴리스 날짜|버전 옵션|빌드|
|:---|:---|:---|:---|:---|
|Windows|[설치 관리자](https://go.microsoft.com/fwlink/?linkid=875508)|2018 1 월 25,|17.4.1|14.0.3917.1|
|macOS (미리 보기)|[.zip](https://go.microsoft.com/fwlink/?linkid=873927)|2018 년 5 월 9, |0.0.1|15.0.4057.1|
|Linux(미리 보기)|[.zip](https://go.microsoft.com/fwlink/?linkid=873926)|2018 년 5 월 9, |0.0.1|15.0.4057.1|

## <a name="get-sqlpackage-for-windows"></a>Sqlpackage Windows에 대 한 가져오기

이 릴리스의 sqlpackage 표준 Windows 설치 관리자 환경 및.zip 포함합니다. 

**설치 관리자**

1. 다운로드 및 실행 된 [DacFramework.msi Windows 용 설치 관리자](https://go.microsoft.com/fwlink/?linkid=875508)합니다.
2. 새 명령 프롬프트 창을 열고 sqlpackage.exe 실행
    - sqlpackage는에 설치 되는 ```C:\Program Files\Microsoft SQL Server\140\DAC\bin``` 폴더

## <a name="get-sqlpackage-preview-for-macos"></a>Sqlpackage (미리 보기) macOS에 대 한 가져오기

1. 다운로드 [macOS에 대 한 sqlpackage](https://go.microsoft.com/fwlink/?linkid=873927)합니다.
2. 파일 압축을 풀고 sqlpackage를 시작, 새 터미널 창을 열고을 다음 명령을 입력 합니다.

   **.zip 설치:**
   ```bash 
   mv ~/Downloads/sqlpackage-linux-<version string> ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage 
   ``` 

## <a name="get-sqlpackage-preview-for-linux"></a>Linux 용 sqlpackage (미리 보기) 가져오기

1. 다운로드 [Linux 용 sqlpackage](https://go.microsoft.com/fwlink/?linkid=873926) 설치 관리자 또는 tar.gz 보관 파일 중 하나를 사용 하 여:
2. 파일 압축을 풀고 sqlpackage를 시작, 새 터미널 창을 열고을 다음 명령을 입력 합니다.

   **.zip 설치:**
   ```bash 
   cd ~ 
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bashrc
   source ~/.bashrc 
   sqlpackage 
   ``` 

   > [!NOTE]
   > Debian, Redhat, 및 Ubuntu에서 누락 된 종속성을 할 수 있습니다. 다음 명령을 사용 하 여 linux 버전에 따라 이러한 종속성을 설치 합니다.
   

   **Debian:** 
   ```bash
   sudo apt-get install libuwind8
   ```

   **Redhat:** 
   ```bash
   yum install libunwind 
   yum install libicu 
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   sudo apt-get install libicu52      # for 14.x
   sudo apt-get install libicu55      # for 16.x
   sudo apt-get install libicu57      # for 17.x
   sudo apt-get install libicu60      # for 18.x
   ```


## <a name="uninstall-sqlpackage-preview"></a>Sqlpackage (미리 보기)를 제거 합니다.

Windows installer를 사용 하 여 sqlpackage를 설치한 경우 동일한 방식으로 모든 Windows 응용 프로그램 제거를 제거 합니다.

Sqlpackage.zip 또는 다른 보관을 설치한 경우 다음 단순히 파일을 삭제 합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

sqlpackage는 Windows, macOS 등 및 Linux에서 실행 되며 다음 플랫폼에서 지원 합니다.

### <a name="windows"></a>Windows
- Windows 10
- Windows 8.1 
- Windows 8 
- Windows 7 SP1 
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012 
- Windows Server 2008 R2

### <a name="macos"></a>macOS
- macOS 10.13 높은 시에라
- macOS 10.12 시에라

### <a name="linux-x64"></a>Linux (x64)
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- 에 대 한 자세한 내용은 [sqlpackage](sqlpackage.md)

[Microsoft 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkId=521839)
