---
title: 를 다운로드하여 설치합니다
titleSuffix: Azure Data Studio
description: 다운로드 및 Windows에 대 한 Azure 데이터 Studio 설치, macOS 또는 Linux
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: b8de39cd3039c24420325dbff5ffb3f1db4efd40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801849"
---
# <a name="download-and-install-azure-data-studio"></a>Azure Data Studio 다운로드 및 설치

[!INCLUDE[name-sos](../includes/name-sos.md)]는 Windows, macOS, Linux에서 실행됩니다.


다운로드 하 고 최신 릴리스를 설치 합니다 *6 월 릴리스의*:

> [!NOTE]
> SQL Operations Studio를 통해 업데이트하고 설정, 바로 가기 키 또는 코드 조각을 유지하려는 경우 [사용자 설정 이동](#move-user-settings)을 확인합니다.

|플랫폼|다운로드|릴리스 날짜| 버전 |
|:---|:---|:---|:---|
|Windows|[사용자 설치 관리자 (권장)](https://go.microsoft.com/fwlink/?linkid=2094100)<br>[시스템 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2094200)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2094201)|2019 년 6 월 6 일 |1.8.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2094202)|2019 년 6 월 6 일 |1.8.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2094203)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2094102)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2094101)|2019 년 6 월 6 일 |1.8.0|

최신 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes.md)를 참조하십시오.

## <a name="get-azure-data-studio-for-windows"></a>Windows에 대한 Azure Data Studio 가져오기

이 릴리스의 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 표준 Windows 설치 관리자 환경 및.zip 파일을 포함 합니다.

합니다 *사용자 설치 관리자* 이 필요 하지 않으므로 관리자 권한으로 설치 및 업그레이드를 간소화 하는 것이 좋습니다. 사용자 설치 관리자를 관리자 권한 사용자 로컬 AppData (LOCALAPPDATA) 폴더 위치는 필요가 없습니다. 사용자 설치 관리자는 또한 원활 하 게 백그라운드 업데이트 환경을 제공 합니다. 자세한 내용은 [Windows에 대 한 사용자 설정](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)합니다.


**사용자 설치 관리자** (권장)

1. 다운로드 및 실행 합니다 [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *사용자* Windows 용 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2094100)합니다.
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.

**시스템 설치 관리자**

1. 다운로드 및 실행 합니다 [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *system* Windows 용 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2094200)합니다.
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.


**zip 파일**

1. [ Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=2094201)을 다운로드합니다.
2. 다운로드한 파일을 찾은 다음 압축을 풉니다.
3. `\azuredatastudio-windows\azuredatastudio.exe`를 실행합니다.


## <a name="get-azure-data-studio-for-macos"></a>MacOS에 대한 Azure Data Studio 가져오기

1. [ macOS용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](https://go.microsoft.com/fwlink/?linkid=2094202)를 다운로드합니다.
2. zip 내용을 확장하기 위해 두 번 클릭합니다.
3. *실행 패드*에서 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 사용할 수 있게 하려면 *Azure Data Studio.app*을 *응용 프로그램* 폴더로 끌어옵니다.


## <a name="get-azure-data-studio-for-linux"></a>Linux 용 Azure Data Studio 받기

1. 아래에서 설치 관리자 또는 tar.gz 보관 파일 중 하나를 사용하여 Linux용 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 다운로드합니다.
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2094203)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2094102)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2094101)
1. 파일을 추출하고 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 실행하기 위해 새 터미널 창을 열고 다음 명령을 입력합니다.

   **Debian 설치:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **rpm 설치:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **tar.gz 설치:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > Debian, Redhat 및 Ubuntu에서는 누락된 종속성이 있을 수 있습니다. 다음 명령을 사용하여 Linux 버전에 따라 해당 종속성을 설치합니다.
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
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


## <a name="uninstall-azure-data-studio"></a>Azure Data Studio 제거

Windows 설치 관리자를 사용하여 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 설치한 경우 Windows 응용 프로그램을 제거하는 방식과 동일한 방식으로 제거합니다.

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 .zip 또는 다른 압축 파일을 사용하여 설치한 경우 해당 파일을 단순히 삭제합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 Windows, macOS 및 Linux에서 실행되며 다음 플랫폼에서 지원됩니다.

### <a name="windows"></a>Windows
- Windows 10(64비트)
- Windows 8.1(64비트)
- Windows 8(64비트)
- Windows 7 (SP1) (64 비트) - [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767) 필요
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

## <a name="recommended-system-requirements"></a>권장 시스템 요구 사항
최적의 경험, 권장된 시스템 요구 사항을 사용 하세요.
[업데이트 여기 메모리 수를 수치화 해야 함]

|             | CPU 코어 | 메모리/RAM |
|:-----------|:---------|:----------|
| 권장 |     4     |      8GB    |
|   최소   |     2     |      4GB     |
|             |           |            |

## <a name="check-for-updates"></a>업데이트 확인
최신 업데이트를 확인하려면 창 왼쪽 아래에 있는 기어 아이콘을 클릭한 다음 **업데이트 확인**을 클릭합니다.

## <a name="supported-sql-offerings"></a>지원되는 SQL 서비스

* 이 버전의 Azure 데이터 Studio는 모든 협력 [지원 되는 SQL Server 2014-버전 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ](https://support.microsoft.com/lifecycle?C2=1044) 하 고 Azure SQL Database 및 Azure SQL Data Warehouse의 최신 클라우드 기능을 사용 하 여 작업에 대 한 지원을 제공 합니다. Azure Data Studio는 또한 Azure SQL 관리 되는 인스턴스에 대 한 미리 보기 지원을 제공합니다.

## <a name="upgrade-from-sql-operations-studio"></a>SQL Operations Studio 업그레이드

여전히 SQL Operations Studio 사용 하는 경우 Azure Data Studio로 업그레이드 해야 합니다. SQL Operations Studio 미리 보기 이름 및 미리 보기 버전의 Azure 데이터 Studio 했습니다. 2018 년 5 월 9 월 했습니다 [Azure Data Studio로 이름 변경](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) GA (일반 공급) 버전을 출시 하 고 있습니다. 때문에 SQL Operations Studio 업데이트 또는 지원, 모든 SQL Operations Studio 사용자에 게 문의할 최신 기능, 보안 업데이트를 가져오려는 Azure Data Studio의 최신 버전을 다운로드 하려면 더 이상 수정 합니다.
 
이전 미리 보기에서 최신 Azure Data Studio로 업그레이드 하는 경우 현재 설정 및 확장 손실 됩니다. 설정으로 이동 하려면 다음에서 지침을 따릅니다 *사용자 설정 이동* 섹션:


## <a name="move-user-settings"></a>이동 사용자 설정

사용자 지정 설정, 바로 가기 키 또는 코드 조각을 이동하려는 경우 다음 단계를 수행합니다. 이 Azure Data studio 버전에서 업그레이드하는 경우 작업을 수행하는 것이 중요 합니다.

*이미 Azure Data Studio 또는 되지 설치 했거나 SQL Operations Studio 사용자 지정 하는 경우이 섹션을 무시할 수 있습니다.*


1. 왼쪽 아래에서 기어를 클릭하고 **설정**을 클릭하여 설정을 엽니다.

   ![open-settings](./media/download/open-settings.png)

2. 마우스 오른쪽 단추로 클릭 합니다 **사용자 설정** 위쪽에 탭을 클릭 **탐색기에 표시**

   ![reveal-in-explorer](./media/download/reveal-in-explorer.png)

3. 이 폴더에 있는 모든 파일을 복사하고 문서 폴더와 같은 로컬 드라이브의 위치를 찾기 쉽게 저장합니다.

   ![copy-settings](./media/download/copy-settings.png)

4. 새 버전의 Azure Data Studio, 1-2, 3단계에 대한 다음 폴더에 저장한 콘텐츠를 붙여넣습니다. 단계를 수행합니다. 수동으로 설정, 키 바인딩 또는 해당 위치로의 코드 조각은 복사할 수 있습니다.

5. 기존 설치를 재정의 하는 경우 리소스 탐색기에 대 한 Azure 계정에 연결 하는 오류를 방지 하기 위해 설치 하기 전에 이전 설치 디렉터리를 삭제 합니다.

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 중 하나를 참조 하세요.
- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL 데이터베이스 연결 및 쿼리](quickstart-sql-database.md)
- [Azure 데이터 웨어하우스 연결 및 쿼리](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Microsoft 개인정보취급방침](https://go.microsoft.com/fwlink/?LinkId=521839) 및 [사용 현황 데이터 수집](usage-data-collection.md).