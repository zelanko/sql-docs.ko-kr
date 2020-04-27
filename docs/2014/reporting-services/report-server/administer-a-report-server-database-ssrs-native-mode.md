---
title: 보고서 서버 데이터베이스 관리(SSRS 기본 모드) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- renaming databases
- report server database
- databases [Reporting Services], administering
- reportservertempdb
- reportserver database
ms.assetid: 97b2e1b5-3869-4766-97b9-9bf206b52262
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d155437880f1fb93779a2352bd507ea83de16256
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104276"
---
# <a name="administer-a-report-server-database-ssrs-native-mode"></a>보고서 서버 데이터베이스 관리(SSRS 기본 모드)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포는 두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스를 내부 스토리지로 사용합니다. 기본적으로 데이터베이스 이름은 각각 ReportServer와 ReportServerTempdb입니다. ReportServerTempdb는 기본 보고서 서버 데이터베이스로 생성되며 임시 데이터, 세션 정보 및 캐시된 보고서를 저장하는 데 사용됩니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 데이터베이스 관리 태스크에는 보고서 서버 데이터베이스를 백업 및 복원하고 중요한 데이터의 암호화 및 암호 해독에 사용되는 암호화 키를 관리하는 작업이 포함됩니다.  
  
 보고서 서버 데이터베이스의 관리를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 다양한 도구를 제공합니다.  
  
-   보고서 서버 데이터베이스를 백업/복원, 이동 또는 복구하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령 또는 데이터베이스 명령 프롬프트 유틸리티를 사용합니다. 자세한 내용은 SQL Server 온라인 설명서의 [다른 컴퓨터로 보고서 서버 데이터베이스 이동&#40;SSRS 기본 모드&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)을 참조하세요.  
  
-   기존 데이터베이스 내용을 다른 보고서 서버 데이터베이스에 복사하려면 다른 보고서 서버 인스턴스에 보고서 서버 데이터베이스의 복사본을 연결하여 사용합니다. 또는 SOAP 호출을 사용하는 스크립트를 만들어서 실행하여 새 데이터베이스에 보고서 서버 내용을 다시 만들 수 있습니다. **rs** 유틸리티를 사용하여 스크립트를 실행할 수 있습니다.  
  
-   보고서 서버와 보고서 서버 데이터베이스 간의 연결을 관리하고 특정 보고서 서버 인스턴스에 사용되는 데이터베이스를 알아보려면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]구성 도구의 데이터베이스 설치 페이지를 사용합니다. 보고서 서버 데이터베이스에 보고서 서버 연결에 대한 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)을 참조하세요.  
  
## <a name="sql-server-login-and-database-permissions"></a>SQL Server 로그인 및 데이터베이스 권한  
 보고서 서버 데이터베이스는 보고서 서버에 의해 내부에서 사용됩니다. 두 데이터베이스에 대한 연결은 보고서 서버 서비스에 의해 설정됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 보고서 서버 데이터베이스에 대한 보고서 서버 연결을 구성합니다.  
  
 데이터베이스에 대한 보고서 서버 연결의 자격 증명은 서비스 계정, Windows 로컬 또는 도메인 계정, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 사용자일 수 있습니다. 연결의 기존 계정을 선택해야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 사용자를 위해 계정을 만들지 않습니다.  
  
 보고서 서버 데이터베이스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 사용자가 지정하는 계정에 대해 자동으로 만들어집니다.  
  
 데이터베이스 권한도 자동으로 구성됩니다. Reporting Services 구성 도구는 보고서 서버 데이터베이스에 대한 `Public` 및 `RSExecRole` 역할에 계정이나 데이터베이스 사용자를 할당합니다. `RSExecRole`은 데이터베이스 테이블에 액세스하고 저장 프로시저를 실행할 수 있는 권한을 제공합니다. 는 `RSExecRole` 보고서 서버 데이터베이스를 만들 때 master 및 msdb에 생성 됩니다. `RSExecRole`은 보고서 서버 데이터베이스에 대한 `db_owner` 역할의 멤버로, 보고서 서버가 자동 업그레이드 프로세스를 지원하기 위해 고유한 스키마를 업데이트할 수 있도록 합니다.  
  
## <a name="naming-conventions-for-the-report-server-databases"></a>보고서 서버 데이터베이스의 명명 규칙  
 주 데이터베이스를 만들 때 데이터베이스의 이름은 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)에 대해 지정된 규칙을 따라야 합니다. 임시 데이터베이스 이름은 항상 주 보고서 서버 데이터베이스와 같은 이름을 사용하되 Tempdb 접미사를 포함합니다. 임시 데이터베이스의 이름은 다르게 선택할 수 없습니다.  
  
 보고서 서버 데이터베이스는 내부 구성 요소로 간주되므로 보고서 서버 데이터베이스의 이름을 바꿀 수 없습니다. 보고서 서버 데이터베이스의 이름을 바꾸면 오류가 발생합니다. 특히 주 데이터베이스의 이름을 바꾸면 데이터베이스 이름이 동기화되지 않았다는 오류 메시지가 표시됩니다. ReportServerTempdb 데이터베이스의 이름을 바꾸면 나중에 보고서를 실행할 때 다음과 같은 내부 오류가 발생합니다.  
  
 "보고서 서버에서 내부 오류가 발생했습니다. 자세한 내용은 오류 로그를 참고하세요. (rsInternalError)  
  
 개체 이름 'ReportServerTempDB.dbo.PersistedStream'이 잘못되었습니다."  
  
 이 오류는 ReportServerTempdb 이름이 내부적으로 저장되어 내부 작업을 수행하는 저장 프로시저에서 사용되기 때문에 발생합니다. 임시 데이터베이스의 이름을 바꾸면 저장 프로시저가 제대로 작동할 수 없습니다.  
  
## <a name="enabling-snapshot-isolation-on-the-report-server-database"></a>보고서 서버 데이터베이스에서 스냅샷 격리 사용  
 보고서 서버 데이터베이스에서는 스냅샷 격리를 사용할 수 없습니다. 스냅샷 격리를 설정하면 “선택한 보고서는 아직 볼 수 없습니다. 보고서를 렌더링하고 있거나 보고서 스냅샷을 사용할 수 없습니다"라는 오류가 발생합니다.  
  
 스냅샷 격리를 의도적으로 사용하지 않은 경우 다른 애플리케이션이 해당 특성을 설정했거나 **model** 데이터베이스가 스냅샷 격리를 사용할 수 있도록 설정되어 모든 새 데이터베이스가 해당 설정을 상속하는 것일 수 있습니다.  
  
 보고서 서버 데이터베이스에서 스냅샷 격리를 해제하려면 Management Studio를 시작하고 새 쿼리 창을 연 후 다음 스크립트를 붙여넣어 실행합니다.  
  
```  
ALTER DATABASE ReportServer  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServerTempdb  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServer  
SET READ_COMMITTED_SNAPSHOT OFF  
ALTER DATABASE ReportServerTempDb  
SET READ_COMMITTED_SNAPSHOT OFF  
```  
  
## <a name="about-database-versions"></a>데이터베이스 버전 정보  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 데이터베이스 버전에 대한 명시적인 정보를 사용할 수 없습니다. 그러나 데이터베이스 버전이 항상 제품 버전과 동기화되므로 제품 버전 정보를 사용하여 데이터베이스 버전 변경 여부를 알 수 있습니다. 에 대 한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 제품 버전 정보는 로그 파일에 표시 되는 파일 버전 정보, 모든 SOAP 호출의 헤더 및 보고서 서버 URL에 연결 하는 경우 (예:에 http://localhost/reportserver)대 한 브라우저를 열 때)를 통해 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [기본 모드 보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [보고서 서버 서비스 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Reporting Services 백업 및 복원 작업](../install-windows/backup-and-restore-operations-for-reporting-services.md)   
 [보고서 서버 데이터베이스&#40;SSRS 기본 모드&#41;](report-server-database-ssrs-native-mode.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](reporting-services-report-server-native-mode.md)   
 [암호화된 보고서 서버 데이터 저장&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [암호화 키 구성 및 관리&#40;SSRS 구성 관리자&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
