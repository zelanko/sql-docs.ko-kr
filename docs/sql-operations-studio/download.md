---
title: Microsoft SQL Operations Studio (preview) 다운로드 및 설치 | Microsoft Docs
description: Microsoft SQL Operations Studio (preview) 를 Windows, macOS, 또는 Linux에 다운로드 및 설치합니다.
ms.custom: tools|sos
ms.date: 03/28/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bf4e79bc1f7092ebe95ff29079f3412306cf7b1
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2018
---
# <a name="download-and-install-sql-operations-studio-preview"></a>SQL Operations Studio (preview) 다운로드 및 설치

[!INCLUDE[name-sos](../includes/name-sos.md)]는 Windows, macOS, Linux에서 실행됩니다.

*2월 공개 미리 보기* 에서 최신 릴리스를 다운로드 및 설치합니다.

|플랫폼|다운로드|릴리스 날짜| 버전 |
|:---|:---|:---|:---|
|Windows|[설치 관리자](https://go.microsoft.com/fwlink/?linkid=870837)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=870838)|2018년 3월 28일 |0.27.3|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=870839)|2018년 3월 28일 |0.27.3|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=870842)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=870841)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=870840)|2018년 3월 28일 |0.27.3|

최신 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes.md)를 참조하십시오.

## <a name="get-sql-operations-studio-preview-for-windows"></a>Windows용 SQL Operations Studio (preview) 얻기

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 릴리스에는 표준 Windows 설치 관리자 경험 및 .zip을 포함합니다. 

**설치 관리자**

1. [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows용 설치 관리자](https://go.microsoft.com/fwlink/?linkid=870837)를 다운로드한 다음 실행합니다.
1. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.


**.zip 파일**

1. [ Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=870838)을 다운로드합니다.
2. 다운로드한 파일을 찾은 다음 압축을 풉니다.
3. `\sqlops-windows\sqlops.exe`를 실행합니다.


## <a name="get-sql-operations-studio-preview-for-macos"></a>MacOS용 SQL Operations Studio (preview) 얻기

1. [ macOS용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](https://go.microsoft.com/fwlink/?linkid=870839)를 다운로드합니다.
2. zip 내용을 확장하기 위해 두 번 클릭합니다.
3. [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 *Launchpad*에서 사용할 수 있게 하려면 *sqlops.app*을 *응용 프로그램* 폴더에 드래그합니다.


## <a name="get-sql-operations-studio-preview-for-linux"></a>Linux용 SQL Operations Studio (preview) 얻기

1. 다운로드 [! 포함[이름 sos](../includes/name-sos-short.md) 설치 관리자 또는 tar.gz 보관 파일 중 하나를 사용 하 여 Linux 용:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=870842)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=870841)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=870840)
1. 파일을 추출하고 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 실행하기 위해 새 터미널 창을 열고 다음 명령을 입력합니다.

   **Debian 설치:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
   ```

   **rpm 설치:**
   ```bash
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
   ```

   **tar.gz 설치:**
   ```bash 
   cd ~ 
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~ 
   tar -xvf ~/sqlops-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   sqlops 
   ``` 

   > [!NOTE]
   > Debian, Redhat 및 Ubuntu에서는 누락된 종속성이 있을 수 있습니다. 다음 명령을 사용하여 Linux 버전에 따라 해당 종속성을 설치합니다.
   

   **Debian:** 
   ```bash
   sudo apt-get install libuwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```


## <a name="uninstall-sql-operations-studio-preview"></a>SQL Operations Studio (preview) 제거

Windows 설치 관리자를 사용하여 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 설치한 경우 Windows 응용 프로그램을 제거하는 방식과 동일한 방식으로 제거합니다.

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 .zip 또는 다른 압축 파일을 사용하여 설치한 경우 해당 파일을 단순히 삭제합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 Windows, macOS 및 Linux에서 실행되며 다음 플랫폼에서 지원됩니다.


### <a name="windows"></a>Windows
- Windows 10(64비트)
- Windows 8.1(64비트)
- Windows 8(64비트)
- Windows 7 (SP1) (64 비트) - [KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767) 필요
- Windows Server 2016
- Windows Server 2012 R2(64비트)
- Windows Server 2012(64비트)
- Windows Server 2008 R2(64비트)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra

- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="check-for-updates"></a>업데이트 확인
최신 업데이트를 확인하려면 창 왼쪽 아래에 있는 기어 아이콘을 클릭한 다음 **업데이트 확인**을 클릭합니다.

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 퀵 스타트 중 하나를 참조 합니다.
- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL 데이터베이스 연결 및 쿼리](quickstart-sql-database.md)
- [Azure 데이터 웨어하우스 연결 및 쿼리](quickstart-sql-dw.md)

[!INCLUDE[name-sos](../includes/name-sos-short.md)]에 기여하기:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Microsoft 개인정보취급방침](https://go.microsoft.com/fwlink/?LinkId=521839) 및 [사용 현황 데이터 수집](usage-data-collection.md).
