---
title: 일정 속성(보고서 페이지) | Microsoft Docs
description: SQL Server Management Studio에서 특정 공유 일정에 대한 모든 보고서를 나열하는 Reporting Services 일정 속성 페이지에 대해 알아봅니다.
ms.date: 06/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 155df0fc52ffc390a0bf528fb2a907751dbbfe6b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916899"
---
# <a name="schedule-properties-reports-page"></a>일정 속성(보고서 페이지)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 의 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 일정 속성 페이지를 사용하여 특정 공유 일정을 사용하는 모든 보고서 목록을 볼 수 있습니다. 일정을 사용하여 보고서 스냅샷을 새로 고치거나, 보고서 기록을 생성하거나, 구독을 트리거하거나, 보고서의 캐시된 복사본을 만료시킬 수 있습니다. 일정 사용 방법을 확인하려면 보고서의 속성 및 구독 정보를 확인하십시오.  
  
 이 페이지는 공유 일정을 사용하는 각 보고서를 표시하지만 단일 보고서 내에서 공유 일정이 사용된 횟수는 나타나지 않습니다. 예를 들어 Company Sales 보고서에 대한 20명의 구독자가 모두 동일한 공유 일정을 사용하여 구독 처리를 트리거한다고 가정해 보십시오. 이 경우 Company Sales 보고서에는 20개의 공유 일정에 대한 참조가 있지만 보고서는 이 목록에 한 번만 나타납니다.  
  
 일정 속성 페이지를 열려면
 1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작합니다.
 2. 보고서 서버에 연결합니다.
 3. **공유 일정** 폴더를 엽니다.
 4. 공유 일정을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
 5. **보고서**를 클릭합니다.  
  
  **웹 포털의** 사이트 설정 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 에서 공유 일정을 관리할 수도 있습니다.
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2017의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **폴더**  
 보고서의 경로를 지정합니다.  
  
 **Report**  
 일정을 사용하는 보고서의 이름을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [일정 만들기, 수정 및 삭제](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [일정](../../reporting-services/subscriptions/schedules.md)   
 [Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [일반적인 보고서 속성 구성(보고서 관리자)](https://msdn.microsoft.com/10b941b2-28e6-4408-9ee4-acebc63c8496)  
  
  

