---
title: 설치 마법사에서 SQL Server 2016 설치(설치 프로그램) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 32f7c238a08a7da31d455421ca9fc00d0f8d6bdb
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962369"
---
# <a name="install-sql-server-from-the-installation-wizard-setup"></a>설치 마법사에서 SQL Server 설치(설치 프로그램)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 설치 마법사를 통해 SQL Server를 설치하는 방법을 설명합니다. [!INCLUDE[SQLServer2016](../../includes/sssql15-md.md)] 및 [!INCLUDE[SQLServer2017](../../includes/sssqlv14-md.md)]에 적용됩니다.

이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 인스턴스를 설치하는 절차를 단계별로 설명합니다. 설치 마법사는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 설치할 수 있는 단일 기능 트리를 제공하므로 구성 요소를 개별적으로 설치할 필요가 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 개별적으로 설치하려면 [SQL Server 설치](../../database-engine/install-windows/install-sql-server.md#how-to-install-individual-components)를 참조하세요.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 다른 방법은 다음을 참조하세요.  

* [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
* [구성 파일을 사용하여 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
* [SysPrep을 사용하여 SQL Server 설치](../../database-engine/install-windows/install-sql-server-using-sysprep.md)  
* [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
* [설치 마법사를 사용하여 SQL Server 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]
  
## <a name="prerequisites"></a>사전 요구 사항

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하기 전에 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)을 검토합니다.  
  
> [!NOTE]  
> 로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  

::: monikerRange=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"

###  <a name="bkmk_ga_instalpatch"></a> 패치 설치 요구 사항

Microsoft는 SQL Server 2016 및 2017에서 필수 구성 요소로 설치되는 Microsoft Visual C++ 2013 런타임 이진 파일의 문제를 확인했습니다. 업데이트로 이 문제를 해결할 수 있습니다. Visual C++ 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제가 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)의 지침에 따라 해당 컴퓨터에 Visual C++ 런타임 이진 파일에 대한 패치가 필요한지 확인합니다. 

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에는 적용되지 않습니다.

## <a name="to-install-sql-server-2016-and-2017"></a>SQL Server 2016 및 2017을 설치하려면  

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 **Setup.exe**를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더를 찾은 다음, **Setup.exe**를 두 번 클릭합니다.  
  
1. 설치 마법사가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 설치를 만들려면 왼쪽 탐색 영역에서 **설치**를 선택한 다음, **새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 독립 실행형 설치 또는 기존 설치에 기능 추가**를 선택합니다.  

1. **제품 키** 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 평가판 버전을 설치할지 아니면 PID 키가 있는 프로덕션 버전을 설치할지를 나타내는 옵션을 선택합니다. 자세한 내용은 [SQL Server 2017의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.  
  
   계속하려면 **다음**을 선택합니다.

1. **사용 조건** 페이지에서 사용권 계약을 검토합니다. 동의하는 경우 **동의함** 확인란을 선택하고 **다음**을 선택합니다.  

   >[!NOTE]
   > SQL Server에서는 설치 환경 정보뿐만 아니라 기타 사용 현황 및 성능 데이터를 Microsoft의 제품 개선에 도움을 주기 위해 전송합니다. SQL Server 데이터 처리 및 개인 정보 제어에 대해 자세히 알아보려면 [개인정보처리방침](https://privacy.microsoft.com/privacystatement) 및 [SQL Server를 구성하여 Microsoft에 피드백 보내기](https://docs.microsoft.com/sql/sql-server/sql-server-customer-feedback?view=sql-server-2016)를 참조하세요.

1. **전역 규칙** 페이지에서 규칙 오류가 없는 경우 설치 프로그램이 **제품 업데이트** 페이지로 자동으로 진행됩니다.  
  
1. **제어판** > **모든 제어판 항목** > **Windows 업데이트** > **설정 변경**의 **Microsoft 업데이트** 확인란이 선택되어 있지 않으면 **Microsoft 업데이트** 페이지가 다음에 나타납니다. **Microsoft 업데이트** 확인란을 선택하면 Windows 업데이트를 검색할 때 모든 Microsoft 제품의 최신 업데이트를 포함하도록 컴퓨터 설정이 변경됩니다.  

1. **제품 업데이트** 페이지에는 사용 가능한 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 업데이트가 표시됩니다. 제품 업데이트가 검색되지 않으면 설치 프로그램에서 이 페이지가 표시되지 않으며, **설치 파일 설치** 페이지로 자동으로 진행됩니다.  

1. 설치 프로그램의 **설치 파일 설치** 페이지에는 설치 파일의 다운로드, 추출 및 설치 진행률이 표시됩니다. 설치 프로그램의 업데이트가 발견되고 이 업데이트를 포함하도록 지정하면, 해당 업데이트도 함께 설치됩니다. 업데이트가 없는 경우 설치 프로그램이 자동으로 진행됩니다.
  
1. 설치 프로그램의 **설치 규칙** 페이지에서는 설치 프로그램을 실행하는 동안 발생했을 수 있는 잠재적 문제를 확인합니다. 오류가 발생한 경우 자세한 내용을 보려면 **상태** 열에서 항목을 선택합니다. 오류가 발생하지 않으면 **다음**을 선택합니다.

1. 머신에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 처음 설치하는 경우, 설치 프로그램이 **설치 유형** 페이지를 건너뛰고 **기능 선택** 페이지로 바로 이동합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시스템에 이미 설치되어 있으면 **설치 유형** 페이지를 사용하여 새로 설치하거나 기존 설치에 기능을 추가하도록 선택할 수 있습니다. 계속하려면 **다음**을 선택합니다.
  
1. **기능 선택** 페이지에서 설치할 구성 요소를 선택합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 새 인스턴스를 설치하려면 **데이터베이스 엔진 서비스**를 선택합니다.

    기능 이름을 선택하면 **기능 설명** 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 확인란을 자유롭게 조합하여 선택할 수 있습니다. 자세한 내용은 [SQL Server 2016 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md) 또는 [SQL Server 2017 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2017.md)를 참조하세요.
  
     선택한 기능의 필수 구성 요소가 **선택한 기능의 필수 구성 요소** 창에 표시됩니다. 설치되지 않은 필수 구성 요소가 있을 경우 이 절차의 뒷부분에 설명된 설치 단계에서 설치됩니다.  
  
     **기능 선택** 페이지 맨 아래에 있는 필드를 사용하여 공유 구성 요소의 사용자 지정 디렉터리를 지정할 수도 있습니다. 공유 구성 요소의 설치 경로를 변경하려면 대화 상자 맨 아래에 있는 필드에서 경로를 업데이트하거나 **찾아보기**를 선택하여 설치 디렉터리로 이동합니다. 기본 설치 경로는 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]입니다.  
  
     > [!NOTE]
     > 공유 구성 요소에 대해 절대 경로를 지정해야 합니다. 폴더는 압축하거나 암호화해서는 안 됩니다. 매핑된 드라이브는 지원되지 않습니다.  
  
     SQL Server는 공유 기능에 두 개의 디렉터리를 사용합니다.
  
     * 공유 기능 디렉터리  
     * 공유 기능 디렉터리(x86)  
  
     > [!NOTE]
     > 위의 각 옵션에 대해 다른 경로를 지정해야 합니다.  
  
1. 모든 규칙을 통과하면 **기능 규칙** 페이지가 자동으로 진행됩니다.  
  
1. **인스턴스 구성** 페이지에서 기본 인스턴스를 설치할지 또는 명명된 인스턴스를 설치할지 지정합니다. 자세한 내용은 [인스턴스 구성](../../sql-server/install/instance-configuration.md#instance-configuration-page)을 참조하세요.  
  
     * **인스턴스 ID**: 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 이 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 동일한 동작이 기본 인스턴스와 명명된 인스턴스에 모두 적용됩니다. 기본 인스턴스의 경우, 인스턴스 이름과 인스턴스 ID는 MSSQLSERVER입니다. 기본값이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 텍스트 상자에서 다른 값을 지정합니다.  
  
       > [!NOTE]  
       > 일반적인 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 인스턴스의 경우 기본 인스턴스든, 명명된 인스턴스든 관계없이 인스턴스 ID에 기본값을 사용합니다.  
  
       모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩과 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 구성 요소에 적용됩니다.  
  
     * **설치된 인스턴스**: 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 그리드에 표시됩니다. 컴퓨터에 기본 인스턴스가 이미 설치된 경우 명명된 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]인스턴스를 설치해야 합니다.  
  
     설치의 나머지 부분에 대한 워크플로는 설치에 지정한 기능에 따라 달라집니다. 선택 내용에 따라 일부 페이지는 표시되지 않을 수 있습니다. 

1. Polybase 기능을 설치하도록 선택하면 **인스턴스 구성** 페이지 뒤에 표시되는 SQL Server 설정에 **PolyBase 구성** 페이지가 추가됩니다. PolyBase에는 Oracle JRE 7 업데이트 51 이상이 필요하며, 아직 설치하지 않은 경우 설치가 차단됩니다. **PolyBase 구성** 페이지에서 SQL Server를 독립 실행형 PolyBase 사용 인스턴스로 사용하도록 선택하거나, 이 SQL Server를 PolyBase 스케일 아웃 그룹의 일부로 사용할 수 있습니다. 스케일 아웃 그룹을 사용하도록 선택하는 경우 최대 6개 이상의 포트 범위를 지정해야 합니다. 


1. **서버 구성 - 서비스 계정** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 로그온 계정을 지정할 수 있습니다. 이 페이지에서 구성하는 실제 서비스는 설치하도록 선택한 기능에 따라 달라집니다. 구성 설정에 대한 자세한 내용은 [설치 마법사 도움말](../../sql-server/install/instance-configuration.md#serverconfig)을 참조하세요.
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 동일한 로그온 계정을 할당하거나, 각 서비스 계정을 개별적으로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스 해제 여부도 지정할 수 있습니다. 각 서비스에 대해 최소한의 권한을 제공하기 위해 서비스 계정을 개별적으로 구성하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 작업을 완료하는 데 필요한 최소한의 권한만 부여되도록 합니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 서비스 계정에 대해 동일한 로그온 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 입력합니다.  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  

    > [!NOTE]
    > [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터, **SQL Server 데이터베이스 엔진 서비스에 볼륨 유지 관리 작업 권한 부여** 확인란을 선택하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스 계정으로 [데이터베이스 인스턴트 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 사용할 수 있도록 합니다.
  
1. **서버 구성 - 데이터 정렬** 페이지를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 기본이 아닌 데이터 정렬을 지정합니다.    

   기본 설치 설정은 OS(운영 체제) 로캘에 의해 결정됩니다. 설치 도중 서버 수준 데이터 정렬을 변경할 수도 있고, 설치하기 전에 OS 로캘을 변경할 수도 있습니다. 기본 데이터 정렬은 각 특정 로캘에 연결된 사용 가능 버전 중 가장 오래된 버전으로 설정됩니다. 이는 이전 버전과의 호환성을 유지하기 위함이므로 권장되는 데이터 정렬이 아닐 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 활용하려면 Windows 데이터 정렬을 사용하기 위한 기본 설치 설정을 변경하세요. 예를 들어 OS 로캘 **영어(미국)** (코드 페이지 1252)의 경우 설치 중의 기본 데이터 정렬은 **SQL_Latin1_General_CP1_CI_AS**이고 가장 가까운 Windows 데이터 정렬인 **Latin1_General_100_CI_AS_SC**로 변경될 수 있습니다.

   자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
1. **데이터베이스 엔진 구성 – 서버 구성** 페이지를 사용하여 다음 옵션을 지정할 수 있습니다.  
  
    * **보안 모드**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 **Windows 인증** 또는 **혼합 모드 인증**을 선택합니다. **혼합 모드 인증**을 선택하는 경우 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 계정의 강력한 암호를 제공해야 합니다.  
  
       디바이스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 성공적으로 연결되면, Windows 인증과 혼합 모드 인증에 동일한 보안 메커니즘이 적용됩니다. 자세한 내용은 [데이터베이스 엔진 구성 - 서버 구성](../../sql-server/install/instance-configuration.md#serverconfig) 페이지를 참조하세요.
  
    * **SQL Server 관리자**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행 중인 계정을 추가하려면 **현재 사용자 추가**를 선택합니다. 시스템 관리자 목록에서 계정을 추가하거나 제거하려면 **추가** 또는 **제거**를 선택한 다음, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자 권한이 있는 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
     **데이터베이스 엔진 구성 - 데이터 디렉터리** 페이지를 사용하여 기본값이 아닌 설치 디렉터리를 지정할 수 있습니다. 기본 디렉터리에 설치하려면 **다음**을 선택합니다.  
  
    > [!IMPORTANT]  
    > 기본값이 아닌 설치 디렉터리를 지정하는 경우, 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 고유한지 확인합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다.  
  
     자세한 내용은 [데이터베이스 엔진 구성 - 데이터 디렉터리 페이지](../../sql-server/install/instance-configuration.md#datadir)를 참조하세요.

     **데이터베이스 엔진 구성 - TempDB** 페이지를 사용하여 **tempdb**의 파일 크기, 파일 수, 기본값이 아닌 설치 디렉터리, 파일 증가 설정을 구성할 수 있습니다. 자세한 내용은 [데이터베이스 엔진 구성 - TempDB 페이지](../../sql-server/install/instance-configuration.md#tempdb)를 참조하세요. 

 
     **데이터베이스 엔진 구성 - FILESTREAM** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 FILESTREAM을 사용하도록 설정할 수 있습니다. 자세한 내용은 [데이터베이스 엔진 구성 - FILESTREAM 페이지](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream-page)를 참조하세요.  
  
1. **Analysis Services 구성 - 계정 프로비저닝** 페이지를 사용하여 서버 모드와 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 관리자 권한이 있는 사용자 또는 계정을 지정할 수 있습니다. 서버 모드에 따라 해당 서버에서 사용되는 메모리 및 스토리지 하위 시스템이 결정됩니다. 각 솔루션 유형은 서로 다른 서버 모드로 실행됩니다. 서버에서 다차원 큐브 데이터베이스를 실행하려는 경우, 기본 서버 모드 옵션인 **다차원 및 데이터 마이닝**을 선택합니다.

    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 시스템 관리자를 한 명 이상 지정해야 합니다.

    * SQL Server 설치 프로그램을 실행 중인 계정을 추가하려면 **현재 사용자 추가**를 선택합니다.

    * 시스템 관리자 목록에서 계정을 추가하거나 제거하려면 **추가** 또는 **제거**를 선택한 다음, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 관리자 권한이 있는 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.

    서버 모드 및 관리자 권한에 대한 자세한 내용은 [Analysis Services 구성 - 계정 프로비저닝 페이지](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning-page)를 참조하세요.

    목록 편집을 마쳤으면 **확인**을 선택합니다. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록이 완료되었으면 **다음**을 선택합니다.

    **Analysis Services 구성 - 데이터 디렉터리** 페이지를 사용하여 기본값이 아닌 설치 디렉터리를 지정할 수 있습니다. 기본 디렉터리에 설치하려면 **다음**을 선택합니다.  

    > [!IMPORTANT]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 INSTANCEDIR과 SQLUSERDBDIR에 대해 동일한 디렉터리 경로를 지정하면, 권한 누락으로 인해 SQL Server 에이전트 및 전체 텍스트 검색이 시작되지 않습니다.  
    >  
    > 기본값이 아닌 설치 디렉터리를 지정하는 경우, 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 고유한지 확인합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다.  

    자세한 내용은 [Analysis Services 구성 - 데이터 디렉터리 페이지](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories-page)를 참조하세요.  

1. **Distributed Replay Controller 구성** 페이지를 사용하여 Distributed Replay Controller 서비스의 관리 권한을 부여할 사용자를 지정할 수 있습니다. 관리 권한이 있는 사용자는 Distributed Replay Controller 서비스에 무제한으로 액세스할 수 있습니다.  
  
     * SQL Server 설치 프로그램을 실행 중인 사용자에게 Distributed Replay Controller 서비스에 대한 액세스 권한을 부여하려면 **현재 사용자 추가** 단추를 선택합니다.

     * 다른 사용자에게 Distributed Replay Controller 서비스에 대한 액세스 권한을 부여하려면 **추가** 단추를 선택합니다.

     * Distributed Replay Controller 서비스에서 액세스 권한을 제거하려면 **제거** 단추를 선택합니다.

     * 계속하려면 **다음**을 선택합니다.  
  
1. **Distributed Replay Client 구성** 페이지를 사용하여 Distributed Replay Client 서비스의 관리 권한을 부여할 사용자를 지정할 수 있습니다. 관리 권한이 있는 사용자는 Distributed Replay Client 서비스에 무제한으로 액세스할 수 있습니다.  
  
     * **컨트롤러 이름**은 선택 사항입니다. 기본값은 \<‘공백’>입니다.  클라이언트 컴퓨터에서 Distributed Replay Client 서비스를 위해 통신할 컨트롤러의 이름을 입력합니다.  
  
       * 컨트롤러를 이미 설정한 경우, 각 클라이언트를 구성할 때 컨트롤러의 이름을 입력합니다.  
  
       * 컨트롤러를 아직 설정하지 않은 경우에는 컨트롤러 이름을 비워 둡니다. 그러나 **클라이언트 구성** 파일에서 컨트롤러 이름을 수동으로 입력해야 합니다.  
  
     * Distributed Replay Client 서비스의 **작업 디렉터리** 를 지정합니다. 기본 작업 디렉터리는 \<*드라이브 문자*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\입니다.  
  
     * Distributed Replay Client 서비스의 **결과 디렉터리** 를 지정합니다. 기본 결과 디렉터리는 \<*드라이브 문자*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\입니다.  
  
     * 계속하려면 **다음**을 선택합니다.  
  
1. **설치 준비 완료** 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 설치 프로그램의 이 페이지에서는 **제품 업데이트** 기능의 사용 여부와 최종 업데이트 버전이 표시됩니다.  
  
     계속하려면 **설치**를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능의 필수 구성 요소를 먼저 설치한 다음, 선택한 기능을 설치합니다.  
  
1. 설치 중에 **설치 진행률** 페이지에서 제공하는 상태 업데이트를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
1. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다.
  
    > [!IMPORTANT]
    > 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스를 완료하려면 **닫기**를 선택합니다.  
  
1. 컴퓨터를 다시 시작하라는 메시지가 나타나면 다시 시작합니다.

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
## <a name="to-install-sql-server-2019"></a>SQL Server 2019를 설치하려면 
  
1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 미디어를 넣고 루트 폴더에서 **Setup.exe**를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더를 찾은 다음, **Setup.exe**를 두 번 클릭합니다.  
  
1. 설치 마법사가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 실행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 설치를 만들려면 왼쪽 탐색 영역에서 **설치**를 선택한 다음, **새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 독립 실행형 설치 또는 기존 설치에 기능 추가**를 선택합니다.  

1. **제품 키** 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 평가판 버전을 설치할지 아니면 PID 키가 있는 프로덕션 버전을 설치할지를 나타내는 옵션을 선택합니다. 자세한 내용은 [SQL Server 2017의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.  
  
   계속하려면 **다음**을 선택합니다.

  
1. **사용 조건** 페이지에서 사용권 계약을 검토합니다. 동의하는 경우 **사용 조건 및 [개인정보처리방침](https://privacy.microsoft.com/privacystatement)에 동의함** 확인란을 선택하고 **다음**을 선택합니다.  

   >[!NOTE]
   > SQL Server에서는 설치 환경 정보뿐만 아니라 기타 사용 현황 및 성능 데이터를 Microsoft의 제품 개선에 도움을 주기 위해 전송합니다. SQL Server 데이터 처리 및 개인 정보 제어에 대해 자세히 알아보려면 [개인정보처리방침](https://privacy.microsoft.com/privacystatement) 및 [SQL Server를 구성하여 Microsoft에 피드백 보내기](https://docs.microsoft.com/sql/sql-server/sql-server-customer-feedback?view=sql-server-2016)를 참조하세요.

1. **전역 규칙** 페이지에서 규칙 오류가 없는 경우 설치 프로그램이 **제품 업데이트** 페이지로 자동으로 진행됩니다.  
  
1. **제어판** > **모든 제어판 항목** > **Windows 업데이트** > **설정 변경**의 **Microsoft 업데이트** 확인란이 선택되어 있지 않으면 **Microsoft 업데이트** 페이지가 다음에 나타납니다. **Microsoft 업데이트** 확인란을 선택하면 Windows 업데이트를 검색할 때 모든 Microsoft 제품의 최신 업데이트를 포함하도록 컴퓨터 설정이 변경됩니다.  

1. **제품 업데이트** 페이지에는 사용 가능한 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 업데이트가 표시됩니다. 제품 업데이트가 검색되지 않으면 설치 프로그램에서 이 페이지가 표시되지 않으며, **설치 파일 설치** 페이지로 자동으로 진행됩니다.  

1. 설치 프로그램의 **설치 파일 설치** 페이지에는 설치 파일의 다운로드, 추출 및 설치 진행률이 표시됩니다. 설치 프로그램의 업데이트가 발견되고 이 업데이트를 포함하도록 지정하면, 해당 업데이트도 함께 설치됩니다. 업데이트가 없는 경우 설치 프로그램이 자동으로 진행됩니다.
  
1. 설치 프로그램의 **설치 규칙** 페이지에서는 설치 프로그램을 실행하는 동안 발생했을 수 있는 잠재적 문제를 확인합니다. 오류가 발생한 경우 자세한 내용을 보려면 **상태** 열에서 항목을 선택합니다. 오류가 발생하지 않으면 **다음**을 선택합니다.

1. 머신에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 처음 설치하는 경우, 설치 프로그램이 **설치 유형** 페이지를 건너뛰고 **기능 선택** 페이지로 바로 이동합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 시스템에 이미 설치되어 있으면 **설치 유형** 페이지를 사용하여 새로 설치하거나 기존 설치에 기능을 추가하도록 선택할 수 있습니다. 계속하려면 **다음**을 선택합니다.
  
1. **기능 선택** 페이지에서 설치할 구성 요소를 선택합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 새 인스턴스를 설치하려면 **데이터베이스 엔진 서비스**를 선택합니다.

    기능 이름을 선택하면 **기능 설명** 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 확인란을 자유롭게 조합하여 선택할 수 있습니다. 자세한 내용은 [SQL Server 2016 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md) 또는 [SQL Server 2017 버전 및 구성 요소](../../sql-server/editions-and-components-of-sql-server-2017.md)를 참조하세요.
  
     선택한 기능의 필수 구성 요소가 **선택한 기능의 필수 구성 요소** 창에 표시됩니다. 설치되지 않은 필수 구성 요소가 있을 경우 이 절차의 뒷부분에 설명된 설치 단계에서 설치됩니다.  
  
     **기능 선택** 페이지 맨 아래에 있는 필드를 사용하여 공유 구성 요소의 사용자 지정 디렉터리를 지정할 수도 있습니다. 공유 구성 요소의 설치 경로를 변경하려면 대화 상자 맨 아래에 있는 필드에서 경로를 업데이트하거나 **찾아보기**를 선택하여 설치 디렉터리로 이동합니다. 기본 설치 경로는 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]입니다.  
  
     > [!NOTE]
     > 공유 구성 요소에 대해 절대 경로를 지정해야 합니다. 폴더는 압축하거나 암호화해서는 안 됩니다. 매핑된 드라이브는 지원되지 않습니다.  
  
     SQL Server는 공유 기능에 두 개의 디렉터리를 사용합니다.
  
     * 공유 기능 디렉터리  
     * 공유 기능 디렉터리(x86)  
  
     > [!NOTE]
     > 위의 각 옵션에 대해 다른 경로를 지정해야 합니다.  
  
1. 모든 규칙을 통과하면 **기능 규칙** 페이지가 자동으로 진행됩니다.  
  
1. **인스턴스 구성** 페이지에서 기본 인스턴스를 설치할지 또는 명명된 인스턴스를 설치할지 지정합니다. 자세한 내용은 [인스턴스 구성](../../sql-server/install/instance-configuration.md#instance-configuration-page)을 참조하세요.  
  
     * **인스턴스 ID**: 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 이 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 동일한 동작이 기본 인스턴스와 명명된 인스턴스에 모두 적용됩니다. 기본 인스턴스의 경우, 인스턴스 이름과 인스턴스 ID는 MSSQLSERVER입니다. 기본값이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 텍스트 상자에서 다른 값을 지정합니다.  
  
       > [!NOTE]  
       > 일반적인 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 인스턴스의 경우 기본 인스턴스든, 명명된 인스턴스든 관계없이 인스턴스 ID에 기본값을 사용합니다.  
  
       모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩과 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 구성 요소에 적용됩니다.  
  
     * **설치된 인스턴스**: 설치 프로그램을 실행 중인 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 그리드에 표시됩니다. 컴퓨터에 기본 인스턴스가 이미 설치된 경우 명명된 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]인스턴스를 설치해야 합니다.  
  
     설치의 나머지 부분에 대한 워크플로는 설치에 지정한 기능에 따라 달라집니다. 선택 내용에 따라 일부 페이지는 표시되지 않을 수 있습니다. 

1. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 부터는 기능을 설치하기 전에 Polybase에서 더 이상 Oracle JRE 7 업데이트 51(이상)을 컴퓨터에 미리 설치할 필요가 없습니다. Polybase 기능을 설치하도록 선택하면 **인스턴스 구성** 페이지 뒤에 표시되는 SQL Server 설정에 **Java 설치 구성** 페이지가 추가됩니다. Java 설치 위치 페이지에서 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 설치에 포함된 Azul Zulu Open JRE를 설치하도록 선택하거나, 컴퓨터에 이미 설치된 다른 JRE 또는 JDK의 위치를 제공할 수 있습니다.

1. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 Java에 언어 확장이 추가되었습니다. Java 기능을 설치하도록 선택하면 **인스턴스 구성** 페이지 뒤에 표시되는 SQL Server 설정 대화 상자 창에 **Java 설치 위치** 페이지가 추가됩니다. **Java 설치 위치** 페이지에서 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 설치에 포함된 Zulu Open JRE를 설치하도록 선택하거나, 컴퓨터에 이미 설치된 다른 JRE 또는 JDK의 위치를 제공할 수 있습니다.

1. **서버 구성 - 서비스 계정** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 로그온 계정을 지정할 수 있습니다. 이 페이지에서 구성하는 실제 서비스는 설치하도록 선택한 기능에 따라 달라집니다. 구성 설정에 대한 자세한 내용은 [설치 마법사 도움말](../../sql-server/install/instance-configuration.md#serverconfig)을 참조하세요.
  
     모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 동일한 로그온 계정을 할당하거나, 각 서비스 계정을 개별적으로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스 해제 여부도 지정할 수 있습니다. 각 서비스에 대해 최소한의 권한을 제공하기 위해 서비스 계정을 개별적으로 구성하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 작업을 완료하는 데 필요한 최소한의 권한만 부여되도록 합니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
     이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 서비스 계정에 대해 동일한 로그온 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 입력합니다.  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  

    > [!NOTE]
    > [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터, **SQL Server 데이터베이스 엔진 서비스에 볼륨 유지 관리 작업 권한 부여** 확인란을 선택하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스 계정으로 [데이터베이스 인스턴트 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 사용할 수 있도록 합니다.
  
     **서버 구성 - 데이터 정렬** 페이지를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 기본값이 아닌 데이터 정렬을 지정할 수 있습니다. 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
1. **데이터베이스 엔진 구성 – 서버 구성** 페이지를 사용하여 다음 옵션을 지정할 수 있습니다.  
  
    * **보안 모드**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 **Windows 인증** 또는 **혼합 모드 인증**을 선택합니다. **혼합 모드 인증**을 선택하는 경우 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 계정의 강력한 암호를 제공해야 합니다.  
  
       디바이스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 성공적으로 연결되면, Windows 인증과 혼합 모드 인증에 동일한 보안 메커니즘이 적용됩니다. 자세한 내용은 [데이터베이스 엔진 구성 - 서버 구성](../../sql-server/install/instance-configuration.md#serverconfig) 페이지를 참조하세요.
  
    * **SQL Server 관리자**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 시스템 관리자를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행 중인 계정을 추가하려면 **현재 사용자 추가**를 선택합니다. 시스템 관리자 목록에서 계정을 추가하거나 제거하려면 **추가** 또는 **제거**를 선택한 다음, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자 권한이 있는 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
     **데이터베이스 엔진 구성 - 데이터 디렉터리** 페이지를 사용하여 기본값이 아닌 설치 디렉터리를 지정할 수 있습니다. 기본 디렉터리에 설치하려면 **다음**을 선택합니다.  
  
    > [!IMPORTANT]  
    > 기본값이 아닌 설치 디렉터리를 지정하는 경우, 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 고유한지 확인합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다.  
  
     자세한 내용은 [데이터베이스 엔진 구성 - 데이터 디렉터리 페이지](../../sql-server/install/instance-configuration.md#datadir)를 참조하세요.

     **데이터베이스 엔진 구성 - TempDB** 페이지를 사용하여 **tempdb**의 파일 크기, 파일 수, 기본값이 아닌 설치 디렉터리, 파일 증가 설정을 구성할 수 있습니다. 자세한 내용은 [데이터베이스 엔진 구성 - TempDB 페이지](../../sql-server/install/instance-configuration.md#tempdb)를 참조하세요.

     **[!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 - MaxDOP** 페이지를 사용하여 최대 병렬 처리 수준을 지정합니다. 이 설정은 단일 문이 실행 중에 사용할 수 있는 프로세서 수를 결정합니다. 권장 값은 설치 중에 자동으로 계산됩니다. 
     
    > [!NOTE]  
    > 이 페이지는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작하는 설치에서만 사용할 수 있습니다. 
    
    자세한 내용은 [데이터베이스 엔진 구성 - MaxDOP 페이지](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop)를 참조하세요. 

     **데이터베이스 엔진 구성 - 메모리** 페이지를 사용하여 시작 후에 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용할 **최소 서버 메모리** 및 **최대 서버 메모리** 값을 지정합니다. **권장** 옵션을 선택한 후 기본값 또는 계산된 권장 값을 사용하거나 사용자 고유의 값을 수동으로 지정할 수 있습니다.
     
    > [!NOTE]  
    > 이 페이지는 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]로 시작하는 설치에서만 사용할 수 있습니다. 
    
    자세한 내용은 [데이터베이스 엔진 구성 - 메모리 페이지](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory)를 참조하세요. 

     **데이터베이스 엔진 구성 - FILESTREAM** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 FILESTREAM을 사용하도록 설정할 수 있습니다. 자세한 내용은 [데이터베이스 엔진 구성 - FILESTREAM 페이지](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream-page)를 참조하세요.  
  
1. **Analysis Services 구성 - 계정 프로비저닝** 페이지를 사용하여 서버 모드와 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 관리자 권한이 있는 사용자 또는 계정을 지정할 수 있습니다. 서버 모드에 따라 해당 서버에서 사용되는 메모리 및 스토리지 하위 시스템이 결정됩니다. 각 솔루션 유형은 서로 다른 서버 모드로 실행됩니다. 서버에서 다차원 큐브 데이터베이스를 실행하려는 경우, 기본 서버 모드 옵션인 **다차원 및 데이터 마이닝**을 선택합니다.

    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 시스템 관리자를 한 명 이상 지정해야 합니다.

    * SQL Server 설치 프로그램을 실행 중인 계정을 추가하려면 **현재 사용자 추가**를 선택합니다.

    * 시스템 관리자 목록에서 계정을 추가하거나 제거하려면 **추가** 또는 **제거**를 선택한 다음, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 관리자 권한이 있는 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.

    서버 모드 및 관리자 권한에 대한 자세한 내용은 [Analysis Services 구성 - 계정 프로비저닝 페이지](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning-page)를 참조하세요.

    목록 편집을 마쳤으면 **확인**을 선택합니다. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록이 완료되었으면 **다음**을 선택합니다.

    **Analysis Services 구성 - 데이터 디렉터리** 페이지를 사용하여 기본값이 아닌 설치 디렉터리를 지정할 수 있습니다. 기본 디렉터리에 설치하려면 **다음**을 선택합니다.  

    > [!IMPORTANT]  
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 INSTANCEDIR과 SQLUSERDBDIR에 대해 동일한 디렉터리 경로를 지정하면, 권한 누락으로 인해 SQL Server 에이전트 및 전체 텍스트 검색이 시작되지 않습니다.  
    >  
    > 기본값이 아닌 설치 디렉터리를 지정하는 경우, 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 고유한지 확인합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다.  

    자세한 내용은 [Analysis Services 구성 - 데이터 디렉터리 페이지](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories-page)를 참조하세요.  

1. **Distributed Replay Controller 구성** 페이지를 사용하여 Distributed Replay Controller 서비스의 관리 권한을 부여할 사용자를 지정할 수 있습니다. 관리 권한이 있는 사용자는 Distributed Replay Controller 서비스에 무제한으로 액세스할 수 있습니다.  
  
     * SQL Server 설치 프로그램을 실행 중인 사용자에게 Distributed Replay Controller 서비스에 대한 액세스 권한을 부여하려면 **현재 사용자 추가** 단추를 선택합니다.

     * 다른 사용자에게 Distributed Replay Controller 서비스에 대한 액세스 권한을 부여하려면 **추가** 단추를 선택합니다.

     * Distributed Replay Controller 서비스에서 액세스 권한을 제거하려면 **제거** 단추를 선택합니다.

     * 계속하려면 **다음**을 선택합니다.  
  
1. **Distributed Replay Client 구성** 페이지를 사용하여 Distributed Replay Client 서비스의 관리 권한을 부여할 사용자를 지정할 수 있습니다. 관리 권한이 있는 사용자는 Distributed Replay Client 서비스에 무제한으로 액세스할 수 있습니다.  
  
     * **컨트롤러 이름**은 선택 사항입니다. 기본값은 \<‘공백’>입니다.  클라이언트 컴퓨터에서 Distributed Replay Client 서비스를 위해 통신할 컨트롤러의 이름을 입력합니다.  
  
       * 컨트롤러를 이미 설정한 경우, 각 클라이언트를 구성할 때 컨트롤러의 이름을 입력합니다.  
  
       * 컨트롤러를 아직 설정하지 않은 경우에는 컨트롤러 이름을 비워 둡니다. 그러나 **클라이언트 구성** 파일에서 컨트롤러 이름을 수동으로 입력해야 합니다.  
  
     * Distributed Replay Client 서비스의 **작업 디렉터리** 를 지정합니다. 기본 작업 디렉터리는 \<*드라이브 문자*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\입니다.  
  
     * Distributed Replay Client 서비스의 **결과 디렉터리** 를 지정합니다. 기본 결과 디렉터리는 \<*드라이브 문자*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\입니다.  
  
     * 계속하려면 **다음**을 선택합니다.  
  
1. **설치 준비 완료** 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 설치 프로그램의 이 페이지에서는 **제품 업데이트** 기능의 사용 여부와 최종 업데이트 버전이 표시됩니다.  
  
     계속하려면 **설치**를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 선택한 기능의 필수 구성 요소를 먼저 설치한 다음, 선택한 기능을 설치합니다.  
  
1. 설치 중에 **설치 진행률** 페이지에서 제공하는 상태 업데이트를 통해 설치 진행률을 모니터링할 수 있습니다.  
  
1. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 **완료** 페이지에 제공됩니다.
  
    > [!IMPORTANT]
    > 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스를 완료하려면 **닫기**를 선택합니다.  
  
1. 컴퓨터를 다시 시작하라는 메시지가 나타나면 다시 시작합니다.

::: moniker-end

## <a name="next-steps"></a>다음 단계

[새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 구성](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-instances-sql-server?view=sql-server-2017)합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 공격받을 수 있는 시스템의 노출 영역을 줄이기 위해 핵심 서비스와 기능을 선별적으로 설치하고 활성화합니다. 자세한 내용은 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:
  
* [SQL Server 설치 유효성 검사](../../database-engine/install-windows/validate-a-sql-server-installation.md)  
* [실패한 SQL Server 설치 복구](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)
* [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
* [설치 마법사를 사용하여 SQL Server로 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
* [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 
