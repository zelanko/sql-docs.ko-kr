---
title: Reporting Services 역할-작업 vs. SharePoint 그룹-사용 권한 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2200027e65978ea0af8cdcc100cda830e8a35881
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75240621"
---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>Reporting Services 역할-작업 vs. SharePoint 그룹-사용 권한
  이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드의 역할 및 태스크 기반 권한 부여 기능과 SharePoint 제품의 보안 기능을 비교해서 보여줍니다. 이 항목에서는 역할, 태스크, SharePoint 그룹, 사용 권한 수준 및 사용 권한의 용어와 특징을 비교합니다.  
  
||  
|-|  
| [!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 &#124; SharePoint 2010 및 SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드|  
  
 **항목 내용**  
  
-   [권한 도구 비교 및 용어](#bkmk_compare_tools_terms)  
  
-   [기본 모드 역할 및 SharePoint 그룹 비교](#bkmk_compare_roles_groups)  
  
-   [기본 모드 태스크 및 SharePoint 권한 비교](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a> 권한 도구 비교 및 용어  
 **기본 모드:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 권한 개체(역할 및 작업)는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 생성되어 보고서 관리자에서 개별 사용자에 대해 구성됩니다.  
  
 **SharePoint 모드:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에는 SharePoint 권한 기능이 사용됩니다. SharePoint 그룹 및 권한은 다음 **사이트 설정** 페이지에서 관리됩니다.  
  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드와 SharePoint 사이의 권한 관련 개체 및 개념을 비교해서 보여줍니다.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드|SharePoint|  
|---------------------------------------------|----------------|  
|**역할:** 예를 들면 "내용 관리자"입니다.|**그룹:** 예를 들면 기본 "뷰어" 그룹입니다.|  
|---|**권한 수준 그룹:** 예를 들면 "뷰어" 그룹의 "보기만"입니다.|  
|**작업:** 예를 들면 "보고서 관리"입니다.|**사용 권한:** 예를 들어 "보기만" 그룹 내에서는 항목 보기, 버전 보기 및 애플리케이션 페이지 보기의 관련 권한이 나열됩니다.|  
  
 SharePoint 권한에 대한 자세한 내용은 [권한 수준 및 권한](https://support.office.com/article/Understand-groups-and-permissions-on-a-SharePoint-site-258E5F33-1B5A-4766-A503-D86655CF950D) 및 [SharePoint 2013의 권한 수준 및 그룹 확인](https://technet.microsoft.com/library/cc262690.aspx)을 참조하세요.  
  
##  <a name="bkmk_compare_roles_groups"></a> 기본 모드 역할 및 SharePoint 그룹 비교  
 다음 표에서는 기본 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에 미리 정의된 역할 정의를 표준 SharePoint 그룹과 비교합니다. SharePoint 그룹이 원하는 특정 역할과 일치하지 않는 경우 SharePoint에서 사용자 지정 그룹을 만들고 사용 권한 수준을 할당할 수 있습니다.  
  
 **참고**: 사용 가능한 기본 SharePoint 그룹은 SharePoint 사이트를 만드는 데 사용되는 사이트 템플릿에 따라 다릅니다.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 역할|SharePoint 그룹|  
|--------------------------------------|-----------------------|  
|**브라우저**<br /><br /> 보기|**방문자** 그룹을 사용하면 보고서를 볼 수 있는 권한을 부여할 수 있습니다. **방문자** 그룹에는 그룹 멤버가 페이지, 목록 항목 및 문서를 볼 수 있는 읽기 수준의 사용 권한이 있습니다.|  
|**내용 관리자**<br /><br /> 보안 설정 권한을 포함하여 모든 항목 및 항목 수준 작업에 대한 모든 권한이 있습니다.|**소유자** 그룹을 사용하여 SharePoint 사이트의 보고서 서버 항목을 관리하는 모든 권한을 부여할 수 있습니다. **소유자** 그룹에는 그룹 멤버가 사이트 콘텐츠, 페이지 또는 기능을 변경할 수 있는 "모든 권한" 사용 권한이 있습니다. 모든 권한은 사이트 관리자에게만 부여해야 합니다.|  
|**내 보고서**|해당하는 그룹이 없습니다. SharePoint 모드로 실행되는 보고서 서버에서는**내 보고서** 가 지원되지 않습니다. 동등한 기능을 사용하려면 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 의 내 사이트 기능을 사용할 수 있습니다.|  
|**게시자**<br /><br /> 보고서, 보고서 모델, 공유 데이터 원본 및 리소스를 추가, 업데이트 및 삭제합니다.|**멤버** 그룹을 사용하여 SharePoint 사이트의 항목을 추가 및 편집하고 종속 항목에 대한 참조를 업데이트하는 권한을 부여할 수 있습니다. **멤버** 그룹에는 그룹 멤버가 페이지를 보고, 항목을 추가 및 업데이트하고, 승인을 받기 위해 변경 내용을 제출할 수 있는 참가 수준의 사용 권한이 있습니다.|  
|**보고서 작성기**<br /><br /> 보고서를 보고, 개별 구독을 자체 관리하고, 보고서 작성기에서 보고서를 엽니다.|보고서 작성기 보고서 정의에 해당하는 미리 정의된 기본 사용 권한 수준이나 SharePoint 그룹이 없습니다. 기본적으로 **멤버** 그룹이나 **소유자** 그룹에 속하는 사용자에게는 보고서 작성기 사용 권한이 있습니다. 더 많은 사용자가 보고서 작성기를 사용할 수 있게 하려면 보고서 작성기 역할이 제공하는 것과 유사한 사용 권한 수준을 제공하는 사용자 지정 보안 설정을 만들어야 합니다. 자세한 내용은 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)을 참조하세요.|  
|-|**뷰어** 그룹을 사용하면 렌더링된 보고서를 볼 수 있는 권한을 부여할 수 있습니다. **뷰어** 그룹은 보고서 항목의 내용을 다운로드하거나 볼 수 없습니다.<br /><br /> **참고:** SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]부터는 **뷰어** 그룹에는 구독을 만들 수 있는 권한이 없습니다.|  
|**시스템 사용자** 및 **시스템 관리자**|이러한 역할은 SharePoint 모드로 실행되는 보고서 서버에는 필요하지 않습니다. **시스템 사용자** 와 **시스템 관리자** 는 SharePoint 팜 또는 웹 애플리케이션 수준의 사용 권한에 해당합니다. 보고서 서버는 해당 수준의 권한 부여에 필요한 기능을 제공하지 않습니다.|  
  
##  <a name="bkmk_compare_tasks_permissions"></a> 기본 모드 태스크 및 SharePoint 권한 비교  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 태스크를 SharePoint 권한과 비교해서 보여줍니다. **유형** 열은 기본 모드 태스크가 시스템 역할 또는 표준 역할과 항목에 관련되어 있는지 여부를 나타냅니다. 시스템 역할은 공유 일정과 같은 시스템 수준의 권한을 관리합니다.  
  
|기본 모드 태스크|역할 유형|해당 SharePoint 권한|  
|----------------------|---------------|--------------------------------------|  
|보고서 사용|항목|항목 편집, 항목 보기|  
|링크된 보고서 만들기|항목|지원되지 않습니다.|  
|모든 구독 관리|항목|경고를 관리합니다.|  
|데이터 원본 관리|항목|항목 추가, 항목 편집, 항목 삭제, 항목 보기|  
|폴더 관리|항목|항목 추가, 항목 편집, 항목 삭제, 항목 보기|  
|개별 구독 관리|항목|항목 편집<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]이전에는 알림 만들기 권한 수준이 필요했습니다.|  
|모델 관리|항목|항목 추가, 항목 편집, 항목 삭제, 항목 보기|  
|보고서 기록 관리|항목|항목 편집, 버전 보기, 버전 삭제|  
|보고서 관리|항목|항목 추가, 항목 편집, 항목 삭제, 항목 보기|  
|리소스 관리|항목|항목 추가, 항목 편집, 항목 삭제, 항목 보기|  
|개별 항목의 보안 설정|항목|사용 권한 관리|  
|데이터 원본 보기|항목|항목 보기|  
|폴더 보기|항목|항목 보기|  
|모델 보기|항목|항목 보기|  
|보고서 보기|항목|항목 보기|  
|리소스 보기|항목|항목 보기|  
||||  
|보고서 정의 실행|시스템|항목 보기|  
|이벤트 생성|시스템|웹 사이트 관리|  
|작업 관리|시스템|없음(지원되지 않음)|  
|보고서 서버 속성 관리|시스템|없음(해당 사항 없음). 보고서 서버는 사용자가 중앙 관리에서 통합 설정을 볼 수 있는지 여부를 제어하지 않습니다.|  
|역할 관리|시스템|사용 권한 관리|  
|공유 일정 관리|시스템|웹 사이트 관리, 열기|  
|보고서 서버 보안 관리|시스템|없음(해당 사항 없음). 보고서 서버는 SharePoint 통합 모드로 실행되는 서버에서 시스템 수준 역할 할당을 사용하지 않습니다.|  
|보고서 서버 속성 보기|시스템|없음(해당 사항 없음). 보고서 서버는 사용자가 중앙 관리에서 통합 설정을 볼 수 있는지 여부를 제어하지 않습니다.|  
|공유 일정 보기|시스템|항목을 엽니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [SharePoint 웹 애플리케이션에서 보고서 서버 작업에 대한 사용 권한 설정](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [역할 정의](../../reporting-services/security/role-definitions.md)   
 [미리 정의된 역할](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
