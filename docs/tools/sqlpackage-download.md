---
title: sqlpackage 다운로드 및 설치 | Microsoft Docs
description: Windows, macOS, 또는 Linux용 sqlpackage 다운로드 및 설치
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
ms.openlocfilehash: 406fb50ceaba177d02bf8d79d0c37191dbe178f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986260"
---
# <a name="download-and-install-sqlpackage"></a>sqlpackage 다운로드 및 설치

sqlpackage는 Windows, macOS 및 Linux에서 실행됩니다.

최신 .NET Framework 릴리스, macOS 및 Linux 미리 보기를 다운로드하고 설치합니다.

|플랫폼|다운로드|릴리스 날짜|버전 옵션|빌드
|:---|:---|:---|:---|:---|
|Windows|[MSI 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2087429)|2019년 4월 15일|18.2|15.0.4384.2|
|macOS .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2087247)|2019년 4월 15일 | 18.2 |15.0.4384.2|
|Linux .NET Core(미리 보기)|[zip 파일](https://go.microsoft.com/fwlink/?linkid=2087431)|2019년 4월 15일 | 18.2 |15.0.4384.2|

최신 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes-sqlpackage.md)를 참조하세요.

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>Windows sqlpackage 가져오기

sqlpackage의 릴리스는 표준 Windows 설치 관리자 환경 및 .zip을 포함하고 있습니다. 

1. [Windows DacFramework.msi 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2087429)를 다운로드하고 실행합니다.
2. 새 명령 프롬프트 창을 열고, sqlpackage.exe을 실행합니다.
    - ```C:\Program Files\Microsoft SQL Server\150\DAC\bin``` 폴더에 sqlpackage가 설치되었습니다.
    - x64 컴퓨터에 x86 버전을 설치하면 ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin``` 폴더에 sqlpackage가 설치됩니다.

## <a name="get-sqlpackage-preview-for-macos"></a>macOS용 sqlpackage 가져오기(미리 보기)

1. [macOS용 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2087247)를 다운로드합니다.
2. 파일을 추출하고 sqlpackage를 실행하려면, 새 터미널 창을 열고 다음 명령을 입력합니다.

   **.zip 설치:**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-preview-for-linux"></a>Linux용 sqlpackage 가져오기(미리 보기)

1. 설치 관리자 또는 tar.gz 아카이브 하나를 사용하여 [Linux용 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2087431)를 다운로드합니다.
2. 파일을 추출하고 sqlpackage를 실행하려면, 새 터미널 창을 열고 다음 명령을 입력합니다.

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
   > Debian, Redhat, 및 Ubuntu에서 종속성 누락을 할 수 있습니다. 다음 명령을 사용하여 Linux 버전에 따라 이러한 종속성을 설치합니다.

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

## <a name="uninstall-sqlpackage-preview"></a>Sqlpackage(미리 보기)를 제거합니다.

Windows installer를 사용하여 sqlpackage를 설치한 경우, 모든 Windows 애플리케이션을 동일한 방식으로 제거합니다.

.zip 또는 다른 아카이브로 sqlpackage를 설치한 경우, 파일을 삭제하기만 하면 됩니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

sqlpackage는 Windows, macOS 및 Linux에서 실행되고, 다음 플랫폼에서 지원됩니다.

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

### <a name="linux-x64"></a>Linux(x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- [sqlpackage](sqlpackage.md)에 대한 자세한 정보

[Microsoft 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkId=521839)
