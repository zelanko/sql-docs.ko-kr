---
title: 시스템 수준 작업 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 52a08acf0e086fbc1db92f6da5ddf0ef8f682433
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43276922"
---
# <a name="tasks-and-permissions---system-level-tasks"></a>작업 및 사용 권한 - 시스템 수준의 작업
  시스템 수준 태스크는 보고서 서버 사이트 전체에 적용되는 작업과 관련된 권한의 모음입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 특정 항목에 적용되는 항목 수준의 태스크도 있습니다. 자세한 내용은 [항목 수준의 태스크](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md)를 참조하세요. 일반적인 태스크 및 사용 권한에 대한 자세한 내용은 [Tasks and Permissions](../../reporting-services/security/tasks-and-permissions.md)을 참조하십시오.  
  
> [!NOTE]  
>  이러한 작업을 프로그래밍 방식으로 수행하는 경우 시스템 수준 태스크를 지원하는 메서드를 사용해야 합니다. 자세한 내용은 <xref:ReportService2010.ReportingService2010.ListTasks%2A> 및 <xref:ReportService2010.ReportingService2010.ListRoles%2A>를 참조하세요.  
  
## <a name="permissions-in-system-level-tasks"></a>시스템 수준 태스크 사용 권한  
 다음 표에서는 각 시스템 태스크에 대한 사용 권한을 보여 줍니다. 나열된 사용 권한은 각 태스크에서 사용 가능한 기능을 보다 정확하게 설명하기 위한 참고용입니다.  
  
|태스크|Permissions|  
|----------|-----------------|  
|보고서 정의 실행|보고서 정의 실행(사용 권한과 태스크 이름이 같음)|  
|이벤트 생성|이벤트 생성|  
|작업 관리|시스템 속성 읽기<br /><br /> 시스템 속성 업데이트|  
|보고서 서버 속성 관리|시스템 속성 읽기<br /><br /> 시스템 속성 업데이트|  
|역할 관리|역할 만들기<br /><br /> 역할 삭제<br /><br /> 역할 속성 읽기<br /><br /> 역할 속성 업데이트|  
|공유 일정 관리|일정 만들기|  
|보고서 서버 보안 관리|시스템 보안 정책 읽기<br /><br /> 시스템 보안 정책 업데이트|  
|보고서 서버 속성 보기|시스템 속성 읽기|  
|공유 일정 보기|일정 읽기|  
  
## <a name="see-also"></a>참고 항목  
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
