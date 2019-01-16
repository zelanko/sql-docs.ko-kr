---
title: 다운로드 및 설치 sqlpackage | Microsoft Docs
description: 다운로드 하 여 Windows, macOS 또는 Linux에 대 한 sqlpackage 설치
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: ba1cb702faef5826158f9f65e9bb36d794934a5a
ms.sourcegitcommit: a11e733bd417905150567dfebc46a137df85a2fa
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991776"
---
# <a name="download-and-install-sqlpackage"></a>다운로드 및 설치 sqlpackage

sqlpackage는 Windows, macOS 및 Linux에서 실행 됩니다.

다운로드 하 여 최신.NET Framework 릴리스 및 macOS 및 Linux 미리 보기를 설치 합니다.

|플랫폼|다운로드|릴리스 날짜|버전 옵션|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2033947)|2018 년 10 월 24 일|18.0|15.0.4200.1|
|macOS.NET Core (미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2044514)|2018년 11월 15일 | - |15.0.4240.1|
|.NET Core Linux (미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2044263)|2018년 11월 15일 | - |15.0.4240.1|

최신 릴리스에 대 한 자세한 내용은 참조는 [릴리스](sqlpackage-release-notes.md)합니다.

## <a name="get-sqlpackage-for-windows"></a>Windows에 대 한 sqlpackage 가져오기

이 버전의 sqlpackage는 표준 Windows 설치 관리자 환경 및.zip을 포함합니다. 

1. 다운로드 및 실행 합니다 [DacFramework.msi Windows 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2033947)합니다.
2. 새 명령 프롬프트 창을 열고 및 sqlpackage.exe를 실행 합니다.
    - sqlpackage를 설치 하기는 ```C:\Program Files\Microsoft SQL Server\150\DAC\bin``` 폴더
    - X86 설치는 x64 버전 sqlpackage 설치는 컴퓨터는 ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin``` 폴더

## <a name="get-sqlpackage-preview-for-macos"></a>Macos (미리 보기) sqlpackage 가져오기

1. 다운로드 [macOS 용 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2044514)합니다.
2. 파일을 추출할 sqlpackage 시작을 새 터미널 창을 열고 다음 명령을 입력 합니다.

   **.zip 설치:**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-preview-for-linux"></a>Linux (미리 보기) sqlpackage 가져오기

1. 다운로드 [Linux 용 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2044263) 설치 관리자 또는 tar.gz 보관 파일 중 하나를 사용 하 여:
2. 파일을 추출할 sqlpackage 시작을 새 터미널 창을 열고 다음 명령을 입력 합니다.

   **.zip 설치:**

   ```bash
   cd ~
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   chmod a+x ~/sqlpackage/sqlpackage
   source ~/.bashrc
   sqlpackage
   ```

   > [!NOTE]
   > Debian, Redhat, 및 Ubuntu에서 종속성 누락을 할 수 있습니다. Linux의 버전에 따라 이러한 종속성을 설치 하려면 다음 명령을 사용 합니다.

   **Debian:**

   ```bash
   sudo apt-get install libunwind8
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

Windows installer를 사용 하 여 sqlpackage를 설치한 경우에 모든 Windows 응용 프로그램을 제거 하면 동일한 방식으로 제거 합니다.

Sqlpackage를.zip 또는 다른 보관을 사용 하 여 설치한 경우 다음 단순히 파일을 삭제 합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

sqlpackage는 Windows, macOS 및 Linux에서 실행 되 고 다음 플랫폼에서 지원 됩니다.

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

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- 자세한 내용은 [sqlpackage](sqlpackage.md)

[Microsoft 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkId=521839)
