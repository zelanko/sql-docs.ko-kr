---
title: 보고서 서버 데이터베이스 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- report server database
- upgrading Reporting Services
ms.assetid: 4091cf87-9d97-4048-a393-67f1f9207401
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3ba4d9ee2e0b92617c2d2bcadae3bf87c8b5414
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108636"
---
# <a name="upgrade-a-report-server-database"></a>보고서 서버 데이터베이스 업그레이드
  보고서 서버 데이터베이스는 하나 이상의 보고서 서버 인스턴스를 위한 스토리지를 제공합니다. 보고서 서버 데이터베이스 스키마는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 새 릴리스마다 변경될 수 있으므로 데이터베이스 버전과 사용하는 보고서 서버 인스턴스 버전이 일치해야 합니다. 대부분의 경우 보고서 서버 데이터베이스는 사용자가 특별한 동작을 수행하지 않고도 자동으로 업그레이드할 수 있습니다.  
  
 **기본 모드:** 기본 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 모드에서는 보고서 서버 데이터베이스가 실제로 기본 이름이 "ReportServer 및 ReportServerTempDB" 인 두 개의 데이터베이스로 구성 됩니다.  
  
 **SharePoint 모드:** SharePoint [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 모드에서는 보고서 서버 데이터베이스가 실제로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 각 인스턴스에 대해 만들어진 데이터베이스 컬렉션입니다.  
  
## <a name="ways-to-upgrade-a-native-mode-report-server-database"></a>기본 모드 보고서 서버 데이터베이스를 업그레이드하는 방법  
 다음 목록에서는 보고서 서버 데이터베이스가 업그레이드되는 조건을 보여 줍니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 보고서 서버의 단일 인스턴스를 업그레이드합니다. 서비스가 시작되고, 보고서 서버에서 데이터 스키마 버전이 서버 버전과 맞지 않는다고 판단되면 보고서 서버 데이터베이스 스키마가 자동으로 업그레이드됩니다.  
  
     서비스를 시작하면 보고서 서버는 데이터베이스 스키마 버전이 서버 버전과 일치하는지 검사합니다. 데이터베이스 스키마가 이전 버전이면 보고서 서버에서 필요한 스키마 버전으로 자동으로 업그레이드됩니다. 자동 업그레이드는 이전 보고서 서버 데이터베이스를 복원 또는 연결한 경우 특히 유용합니다. 이러한 경우 보고서 서버 추적 로그 파일에 데이터베이스 스키마 버전이 업그레이드되었다는 메시지가 기록됩니다.  
  
-   새로운 보고서 서버 인스턴스에서 사용할 이전 버전을 선택하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 로컬 또는 원격 보고서 서버 데이터베이스를 업그레이드합니다. 이 경우 먼저 업그레이드 동작을 확인해야 합니다.  
  
     
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 더 이상 별도의 업그레이드 단추나 업그레이드 스크립트를 제공하지 않습니다. 보고서 서버 서비스의 자동 업그레이드 기능 덕분에 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터는 이러한 기능이 더 이상 사용되지 않습니다.  
  
 스키마를 업데이트한 후에는 이전 버전으로 업그레이드를 롤백할 수 없습니다. 따라서 이전 설치를 다시 만들어야 하는 경우에 대비하여 항상 보고서 서버 데이터베이스를 백업해야 합니다.  
  
## <a name="how-the-schema-metadata-and-report-server-content-is-updated"></a>스키마, 메타데이터 및 보고서 서버 내용을 업데이트하는 방법  
 보고서 서버 데이터베이스는 다음 세 단계로 업그레이드됩니다.  
  
1.  스키마는 설치 또는 서비스 시작 후에 자동으로 업그레이드되거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 이전 버전인 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 보고서 서버 데이터베이스를 선택하면 자동으로 업그레이드됩니다. 또한 보고서 서버 서비스는 시작할 때 데이터베이스 버전을 검사합니다. 보고서 서버가 이전 버전의 데이터베이스와 연결된 경우 보고서 서버는 시작 중에 데이터베이스를 업데이트합니다.  
  
2.  보안 설명자는 스키마가 업데이트된 후 보고서 서버 데이터베이스를 처음 사용할 때 업그레이드됩니다.  
  
3.  게시된 보고서 및 컴파일된 보고서 스냅샷은 처음 사용 시 업데이트됩니다. 자세한 내용은 [Upgrade Reports](upgrade-reports.md)을(를) 참조하세요.  
  
 보고서 서버 데이터베이스 이외에도 보고서 서버는 임시 데이터베이스도 사용합니다. 임시 데이터베이스는 보고서 서버 데이터베이스를 업그레이드할 때 자동으로 업그레이드됩니다.  
  
## <a name="permissions-required-to-upgrade-a-report-server-database"></a>보고서 서버 데이터베이스를 업그레이드하는 데 필요한 사용 권한  
 보고서 서버 데이터베이스가 포함된 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 업그레이드하는 경우 사용 권한이 없는 상태에서 데이터베이스 업그레이드를 수행하면 오류 메시지가 나타날 수 있습니다. 기본적으로 설치 프로그램에서는 해당 설치 프로그램을 실행하는 사용자의 보안 토큰을 사용하여 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하고 스키마를 업데이트합니다. 보고서 서버 데이터베이스를 호스팅하는 데이터베이스 서버에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** 권한이 있으면 데이터베이스가 정상적으로 업그레이드됩니다. 마찬가지로 명령 프롬프트에서 설치 프로그램을 실행하고 원격 컴퓨터에서 스키마를 수정할 수 있는 **sysadmin** 권한이 있는 계정에 대해 RSUPGRADEDATABASEACCOUNT 및 RSUPGRADEPASSWORD 인수를 지정하는 경우에도 데이터베이스가 정상적으로 업그레이드됩니다.  
  
 그러나 원격 컴퓨터의 데이터베이스에 대한 **sysadmin** 권한이 없으면 다음과 같은 오류로 인해 연결이 거부됩니다.  
  
 `"Setup was not able to upgrade the report server database schema. You must update the database schema manually after setup is finished. To update the schema, run the Reporting Services Configuration Manager, open the Database Setup page, re-select the database, and click Apply. The database will be upgraded automatically."`  
  
 이때 보고서 서버 프로그램 파일은 업그레이드되지만 보고서 서버 데이터베이스는 이전 버전의 형식을 유지합니다. 데이터베이스를 수동으로 업그레이드하여 업그레이드 프로세스를 완료할 때까지 보고서 서버는 사용할 수 없습니다.  
  
#### <a name="to-upgrade-a-native-mode-database-with-scripts"></a>스크립트를 사용하여 기본 모드 데이터베이스를 업그레이드하려면  
 WMI 스크립트를 사용하여 보고서 서버 데이터베이스를 업그레이드할 수 있습니다. 자세한 내용은 [GenerateDatabaseUpgradeScript 메서드&#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [보고서 서버 데이터베이스 만들기&#40;SSRS 구성 관리자&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [SSRS 기본 모드 &#40;데이터베이스 변경 마법사&#41;](../../sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [업그레이드 및 마이그레이션 Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [기본 모드로 Reporting Services 설치 &#40;마이그레이션&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
  
