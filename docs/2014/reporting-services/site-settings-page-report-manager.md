---
title: 사이트 설정 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4d67a01c-eae4-49ba-a6e8-8e983c0248f5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3bd40d6b97215329bb2cab060853fc06ef862dbd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065301"
---
# <a name="site-settings-page-report-manager"></a>사이트 설정 페이지(보고서 관리자)
  사이트 설정 페이지를 사용하여 응용 프로그램 제목을 변경하고 보고서 기록 제한 및 보고서 처리 시간 제한 값에 대한 서버 차원 기본값을 설정하고 시스템 수준 역할 할당을 관리하고 공유 일정을 관리할 수 있습니다. 이 페이지를 보려면 내용 관리자 및 시스템 관리자 권한이 있어야 합니다.  
  
> [!NOTE]  
>  일부 SQL Server 버전에서 보고서 기록, 보고서 실행 및 공유 일정 기능은 지원되지 않습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-site-settings-page"></a>사이트 설정 페이지를 열려면  
  
1.  보고서 관리자를 엽니다.  
  
2.  페이지의 맨 위에서 **사이트 설정**을 클릭합니다. 사이트의 일반 속성 페이지가 열립니다.  
  
     **참고:** 보이지 않는 경우는 **사이트 설정** 옵션 메뉴에서 필요가 없습니다 필요한 권한, 자세한 내용은의 "사이트 설정" 섹션을 참조 하세요. [에 대 한 기본 모드 보고서 서버를 구성 합니다. 로컬 관리 &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)합니다.  
  
## <a name="options"></a>변수  
 **이름**  
 이 인스턴스에 사용할 제목을 지정 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 보고서 관리자입니다. 기본적으로 제목은 "[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]"입니다.  
  
 **보고서 기록에 대 한 기본 설정 선택**  
 보관할 보고서 기록 복사본 수로 기본값을 선택합니다. 이 기본값은 보고서 기록 제한을 설정하는 초기 설정이 됩니다. 보고서 수준에서 이 설정을 변경할 수 있습니다. 자세한 내용은 [스냅숏 옵션 속성 페이지&#40;보고서 관리자&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)를 참조하세요.  
  
 나중에 보고서 기록을 제한하면 기존 보고서 기록이 지정한 제한을 초과하는 경우 보고서 서버에서 기존 보고서 기록을 새 제한으로 축소합니다. 가장 오래된 보고서 스냅숏이 먼저 삭제됩니다. 보고서 기록이 비어 있거나 제한보다 적은 경우 새 보고서 스냅숏이 추가됩니다. 한도에 이르면 새 보고서 스냅숏이 추가될 때 가장 오래된 스냅숏이 삭제됩니다.  
  
 **보고서 실행 제한 시간**  
 보고서 처리를 일정 시간(초)으로 제한할지 여부를 지정합니다.  
  
 이 값은 보고서 서버의 보고서 처리에 적용되며, 사용자의 보고서에 데이터를 제공하는 데이터베이스 서버의 데이터 처리에는 영향을 주지 않습니다.  
  
 보고서 처리 시간은 보고서를 선택한 후 보고서가 열리는 데 걸리는 시간입니다. 이 값을 설정할 때는 데이터 처리와 보고서 처리가 모두 완료될 수 있는 시간으로 지정하십시오.  
  
 **사용자 지정 보고서 작성기 시작 URL**  
 보고서 서버에서 기본 보고서 작성기 URL을 사용하지 않는 경우에는 사용자 지정 URL을 지정합니다. 이 설정은 선택 사항입니다. 값을 지정하지 않으면 기본 URL이 사용되어 보고서 작성기가 ClickOnce 응용 프로그램으로 시작됩니다. 기본 URL은 다음 중 하나입니다.  
  
 **기본 모드 보고서 서버:** 기본 모드 설치에서 기본 URL 인 http:// 형식을 따릅니다\<*computername*> / reportserver/ReportBuilder/ReportBuilder_3_0_0_0.application 합니다.  
  
 SharePoint 통합된 모드: 기본 URL 인 http:// 형식을 따릅니다\<*SharePoint_site*> / _vti_bin/ReportBuilder/ReportBuilder_3_0_0_0.application. "  
  
 **적용**  
 변경 내용을 보고서 서버에 저장하려면 클릭합니다.  
  
 **보안**  
 사용자 및 그룹 계정을 미리 정의된 시스템 역할에 할당할 수 있는 시스템 역할 할당 페이지를 열려면 이 링크를 클릭합니다.  
  
 **일정**  
 사용자가 자신의 보고서 및 구독용으로 선택 가능한 공유 일정을 미리 정의할 수 있는 일정 페이지를 열려면 이 링크를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](security/granting-permissions-on-a-native-mode-report-server.md)   
 [미리 정의 된 역할](security/role-definitions-predefined-roles.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
