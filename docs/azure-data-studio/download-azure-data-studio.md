---
title: Azure Data Studio 다운로드 및 설치
description: Windows, macOS, 또는 Linux용 Azure Data Studio를 다운로드 및 설치합니다. 이 문서에서는 릴리스 날짜, 버전 번호, 시스템 요구 사항 및 다운로드 링크를 제공합니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: overview
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: seodec18
ms.date: 9/30/2020
ms.openlocfilehash: 0d318fedc053c4d01db2fc192375c499daa4573d
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987842"
---
# <a name="download-and-install-azure-data-studio"></a>Azure Data Studio 다운로드 및 설치

Azure Data Studio는 Windows, macOS, Linux에서 실행됩니다.

최신 릴리스 다운로드 및 설치:

> [!NOTE]
> SQL Operations Studio에서 업데이트하는 경우 설정, 바로 가기 키 또는 코드 조각을 유지하려면 [사용자 설정 이동](#move-user-settings)을 참조하세요.

|플랫폼|다운로드|릴리스 날짜| 버전 |
|:---|:---|:---|:---|
| Windows | [사용자 설치 관리자(권장)](https://go.microsoft.com/fwlink/?linkid=2144429)<br>[시스템 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2144430)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2144183) | 2020년 9월 30일 | 1.22.1 |
| macOS | [.zip](https://go.microsoft.com/fwlink/?linkid=2144184) | 2020년 9월 30일 | 1.22.1 |
| Linux | [.deb](https://go.microsoft.com/fwlink/?linkid=2144186)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2144185)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2144187) | 2020년 9월 30일| 1.22.1 |

최신 릴리스에 대한 자세한 내용은 [릴리스 정보](./release-notes-azure-data-studio.md)를 참조하세요.

## <a name="get-azure-data-studio-for-windows"></a>Windows용 Azure Data Studio 다운로드

이 Azure Data Studio 릴리스에는 표준 Windows Installer 환경과 .zip 파일이 포함되어 있습니다.

‘사용자 설치 관리자’는 관리자 권한이 필요하지 않기 때문에 설치와 업그레이드가 모두 간소화되므로 권장됩니다. 사용자 설치 관리자는 해당 위치가 사용자 Local AppData(LOCALAPPDATA) 폴더에 있기 때문에 관리자 권한이 필요하지 않습니다. 또한 사용자 설치 관리자는 더 원활한 백그라운드 업데이트 환경을 제공합니다. 자세한 내용은 [Windows용 사용자 설치 프로그램](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)을 참조하세요.

**사용자 설치 관리자**(권장)

1. [Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ‘사용자’ 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2144429)를 다운로드하여 실행합니다.
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.

**시스템 설치 관리자**

1. [Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ‘시스템’ 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2144430)를 다운로드하여 실행합니다.
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.

**zip 파일**

1. [Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=2144183)을 다운로드합니다.
2. 다운로드한 파일로 이동하여 압축을 풉니다.
3. `\azuredatastudio-windows\azuredatastudio.exe`을 실행합니다.

## <a name="get-azure-data-studio-for-macos"></a>macOS용 Azure Data Studio 다운로드

1. [macOS용 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2144184)를 다운로드합니다.
2. zip의 내용을 펼치려면 두 번 클릭합니다.
3. 실행 패드에서 Azure Data Studio를 사용할 수 있게 하려면 *Azure Data Studio.app* 을 *Applications* 폴더로 끌어 놓습니다.

## <a name="get-azure-data-studio-for-linux"></a>Linux용 Azure Data Studio 다운로드

1. 설치 관리자 또는 tar.gz 보관 파일 하나를 사용하여 Linux용 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 다운로드합니다.
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2144186)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2144185)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2144187)
1. 파일을 추출하고 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 시작하려면 새 터미널 창을 열고 다음 명령을 입력합니다.

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
   > Debian, Redhat, 및 Ubuntu에서 종속성 누락을 할 수 있습니다. 다음 명령을 사용하여 Linux 버전에 따라 이러한 종속성을 설치합니다.

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

## <a name="download-insiders-build-of-azure-data-studio"></a>Azure Data Studio 참가자 빌드 다운로드

일반적으로 사용자는 위 Azure Data Studio의 안정적인 릴리스를 다운로드해야 합니다. 그러나 베타 기능을 사용해보고 피드백을 제공하려는 경우 [Azure Data Studio 참가자 빌드](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main)를 다운로드할 수 있습니다.

## <a name="uninstall-azure-data-studio"></a>Azure Data Studio 제거

Windows Installer를 사용하여 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 설치한 경우, Windows 애플리케이션을 제거하는 것과 동일한 방식으로 제거합니다.

.zip 또는 다른 보관 파일을 사용하여 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]를 설치한 경우에는 파일을 삭제하기만 하면 됩니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

Azure Data Studio는 Windows, macOS, Linux에서 실행되고, 다음 플랫폼에서 지원됩니다.

### <a name="windows"></a>Windows

- Windows 10(64비트)
- Windows 8.1(64비트)
- Windows 8(64비트)
- Windows 7(SP1)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2(64비트)
- Windows Server 2012(64비트)
- Windows Server 2008 R2(64비트)

### <a name="macos"></a>macOS

- macOS 10.15 Catalina
- macOS 10.14 Mojave
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="recommended-system-requirements"></a>권장 시스템 요구 사항

| 권장/최소 | CPU 코어 수 | 메모리/RAM |
|---------------------|-----------|------------|
| 권장         |     4     |   8GB     |
|   최소           |     2     |   4GB     |

## <a name="check-for-updates"></a>업데이트 확인

최신 업데이트를 확인하려면 창의 왼쪽 아래에 있는 기어 아이콘을 클릭한 다음, **업데이트 확인**을 클릭합니다.

오프라인 환경에서 업데이트는 이전에 설치된 버전 위에 직접 [최신 버전을 설치](#download-and-install-azure-data-studio)하여 적용할 수 있습니다.  설치 관리자가 현재 설치된 애플리케이션(있는 경우)을 업데이트하므로 이전 버전의 Azure Data Studio를 제거할 필요는 없습니다.

## <a name="supported-sql-offerings"></a>지원되는 SQL 서비스

- 이 Azure Data Studio 버전은 [지원되는 모든 버전의 SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)에서 작동하며 Azure SQL Database와 Azure Synapse Analytics의 최신 클라우드 기능 사용을 지원합니다. Azure Data Studio는 Azure SQL Managed Instance에 대한 미리 보기 지원도 제공합니다.

## <a name="upgrade-from-sql-operations-studio"></a>SQL Operations Studio에서 업그레이드

여전히 SQL Operations Studio를 사용 중인 경우 Azure Data Studio로 업그레이드해야 합니다. SQL Operations Studio는 Azure Data Studio의 미리 보기 이름 및 미리 보기 버전이었습니다. 2018년 9월에 [이름을 Azure Data Studio로 변경](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/)하여 GA(일반 공급) 버전을 릴리스했습니다. SQL Operations Studio는 더 이상 업데이트되거나 지원되지 않으므로 모든 SQL Operations Studio 사용자는 최신 버전의 Azure Data Studio를 다운로드하여 최신 기능, 보안 업데이트 및 수정 프로그램을 사용하시기 바랍니다.

이전 미리 보기에서 최신 Azure Data Studio로 업그레이드하는 경우 현재 설정과 확장이 손실됩니다. 설정을 이동하려면 다음 ‘사용자 설정 이동’ 섹션의 지침을 따르세요.

## <a name="move-user-settings"></a>사용자 설정 이동

사용자 지정 설정, 바로 가기 키 또는 코드 조각을 이동하려면 아래 단계를 수행합니다. SQL Operations Studio 버전에서 Azure Data Studio로 업그레이드하는 경우 이 작업을 수행하는 것이 중요합니다.

‘Azure Data Studio가 이미 있거나 SQL Operations Studio를 설치 또는 사용자 지정한 적이 없는 경우에는 이 섹션을 무시해도 됩니다.’

1. 왼쪽 아래에 있는 기어를 클릭한 다음, **설정**을 클릭하여 설정을 엽니다.

   ![Azure Data Studio에서 설정 편집](./media/download/open-settings.png)

2. 맨 위의 **사용자 설정** 탭을 마우스 오른쪽 단추로 클릭하고 **탐색기에 표시**를 클릭합니다.

   ![로컬 파일 시스템으로 이동할 탐색기 시작](./media/download/reveal-in-explorer.png)

3. 이 폴더의 모든 파일을 복사하고 로컬 드라이브에서 찾기 쉬운 위치(예: 문서 폴더)에 저장합니다.

   ![파일을 사용하여 원하는 위치에 복사](./media/download/copy-settings.png)

4. 최신 버전의 Azure Data Studio에서 1~2단계를 수행하고 3단계에서는, 저장한 내용을 폴더에 붙여넣습니다. 해당 위치에 있는 설정, 키 바인딩 또는 코드 조각 위에 수동으로 복사할 수도 있습니다.

5. 기존 설치를 재정의하는 경우 리소스 탐색기의 Azure 계정에 연결하는 중 오류를 방지하려면 설치 전에 이전 설치 디렉터리를 삭제합니다.

## <a name="next-steps"></a>다음 단계

시작하려면 다음 빠른 시작 중 하나를 참조하세요.

- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)
- [Azure Data Warehouse 연결 및 쿼리](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Microsoft 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkId=521839) 및 [사용량 데이터 수집](usage-data-collection.md)
