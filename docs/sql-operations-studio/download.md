---
title: "Microsoft SQL Operations Studio(미리 보기) 다운로드 및 설치 | Microsoft Docs"
description: "Microsoft SQL Operations Studio(미리 보기)를 Windows, macOS, 또는 Linux에 다운로드 및 설치합니다."
ms.custom: tools|sos
ms.date: 03/05/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1cb41e1824fc157932e2cb08292608bb97e46712
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="download-and-install-sql-operations-studio-preview"></a>SQL Operations Studio(미리 보기) 다운로드 및 설치

[!INCLUDE[name-sos](../includes/name-sos.md)] 는 Windows, macOS, 그리고 Linux에서 실행됩니다.

*2월 공개 미리 보기* 에서 최신 릴리스를 다운로드 및 설치합니다:

|플랫폼|다운로드|릴리스 날짜| 버전 |
|:---|:---|:---|:---|
|Windows|[설치 관리자](https://go.microsoft.com/fwlink/?linkid=867998)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=867997)|2018년 2월 15일 |0.26.7|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=867999)|2018년 2월 15일 |0.26.7|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=868002)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=868001)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=868000)|2018년 2월 15일 |0.26.7|

최신 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes.md) 를 참조합니다.

## <a name="get-sql-operations-studio-preview-for-windows"></a>Windows에서 SQL Operations Studio (미리 보기) 얻기

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 릴리스에는 표준 Windows 설치 관리자 경험 및 .zip을 포함합니다. 

**설치 관리자**

1. [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows용 설치 관리자](https://go.microsoft.com/fwlink/?linkid=867998) 를 다운로드한 다음 실행합니다.
1. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.


**.zip 파일**

1. [ Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=867997) 을 다운로드합니다.
2. 다운로드한 파일을 찾은 다음 압축을 풉니다.
3. `\sqlops-windows\sqlops.exe` 를 실행합니다.


## <a name="get-sql-operations-studio-preview-for-macos"></a>MacOS에서 SQL Operations Studio 얻기

1. [ macOS용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](https://go.microsoft.com/fwlink/?linkid=867999) 을 다운로드합니다.
2. zip 내용을 확장하기 위해 두 번 클릭합니다.
3. [!INCLUDE[name-sos](../includes/name-sos-short.md)] 을 *Launchpad* 에서 사용 가능하도록 하기 위해 *sqlops.app* 을 *응용 프로그램* 폴더에 드래그합니다.


## <a name="get-sql-operations-studio-preview-for-linux"></a>Linux에서 SQL Operations Studio 얻기

1. [ Linux용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](https://go.microsoft.com/fwlink/?linkid=868000) 을 다운로드합니다.
1. 파일을 추출하고 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 을 실행하기 위해, 새 터미널 창을 열고 다음 명령을 입력합니다.

   ```bash
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
   ```

   > [!NOTE]
   > Debian, Redhat 및 Ubuntu 에서는 누락된 종속성이 있을 수 있습니다. 다음 명령을 사용하여 Linux 버전에 따라 해당 종속성을 설치합니다.
   

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


## <a name="uninstall-sql-operations-studio-preview"></a>SQL Operations Studio (미리 보기) 제거

Windows 설치 관리자를 사용하여 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 을 설치한 경우, Windows 응용 프로그램을 제거하는 방식과 동일한 방식으로 제거합니다.

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] .zip 또는 다른 압축 파일을 사용하여 설치한 경우, 해당 파일을 단순히 삭제합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 은 Windows, macOS 및 Linux에서 실행되며 다음 플랫폼에서 지원됩니다.

### <a name="windows"></a>Windows
- Windows 10(64 비트)
- Windows 8.1(64 비트)
- Windows 8(64 비트)
- Windows 7 (SP1) (64 비트) - [KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767) 이 필요합니다
- Windows Server 2016
- Windows Server 2012 R2(64 비트)
- Windows Server 2012(64 비트)
- Windows Server 2008 R2(64 비트)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="check-for-updates"></a>업데이트 확인
최신 업데이트를 확인하려면 창 왼쪽 아래에 있는 기어 아이콘을 클릭한 다음 **업데이트 확인** 을 클릭합니다

## <a name="next-steps"></a>다음 단계

시작하려면 다음 퀵 스타트 중 하나를 참조합니다.
- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL 데이터베이스 연결 및 쿼리](quickstart-sql-database.md)
- [Azure 데이터 웨어하우스 연결 및 쿼리](quickstart-sql-dw.md)

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 에 기여하기:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Microsoft 개인정보취급방침](https://go.microsoft.com/fwlink/?LinkId=521839) 및 [사용 현황 데이터 수집](usage-data-collection.md).
