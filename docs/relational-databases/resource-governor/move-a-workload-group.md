---
title: 작업 그룹 이동 | Microsoft 문서
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties_moveworkloadgroup.f1
helpviewer_keywords:
- workload groups [SQL Server], move
- Resource Governor, workload group move
ms.assetid: f2068636-6e53-486a-a6fc-c12de2a38424
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8d1eb983f32e995d974ffbfb460e679f715d20ac
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="move-a-workload-group"></a>작업 그룹 이동
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 Transact-SQL을 사용하여 리소스 관리자 작업 그룹을 다른 리소스 풀로 이동할 수 있습니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To move a workload group, using:**  [SQL Server Management Studio](#MoveWGSSMS), [Transact-SQL](#MoveWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 보류 중인 리소스 관리자 구성 작업이 있으면 작업 그룹을 이동할 수 없습니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 보류 중인 리소스 관리자 구성 작업이 있으면 작업 그룹을 이동할 수 없습니다. [sys.dm_resource_governor_configuration&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) 동적 관리 뷰를 쿼리해 is_configuration_pending의 현재 상태를 가져와서 보류 중인 구성이 있는지 여부를 확인할 수 있습니다.  
  
###  <a name="Permissions"></a> Permissions  
 작업 그룹을 이동하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="MoveWGSSMS"></a> SQL Server Management Studio를 사용하여 작업 그룹 이동  
 **다음을 사용하여 작업 그룹을 이동하려면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**  
  
1.  개체 탐색기에서 **리소스 관리자** 까지 **관리**노드를 계속 확장합니다.  
  
2.  **Resource Governor** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 그러면 **Resource Governor** 페이지가 열립니다.  
  
3.  **리소스 풀** 창에서 이동할 작업 그룹이 들어 있는 리소스 풀을 클릭합니다. **작업 그룹** 창에 해당 리소스 풀의 작업 그룹이 나열됩니다.  
  
4.  **작업 그룹** 창에서 이동할 작업 그룹의 왼쪽에 있는 오른쪽 화살표를 마우스 오른쪽 단추로 클릭하고 **이동**을 클릭합니다. **작업 그룹 이동** 창이 표시됩니다.  
  
5.  사용 가능한 리소스 풀이 창에 표시됩니다. 작업 그룹을 이동하려는 리소스 풀의 이름을 클릭한 다음 **확인** 을 클릭하여 이동합니다.  
  
6.  **확인**을 클릭하지 않으면 이 동작이 완료되지 않습니다. **확인**을 클릭하면 ALTER RESOURCE GOVERNOR RECONFIGURE 문이 실행됩니다.  
  
7.  리소스 풀이나 작업 그룹의 생성 또는 재구성 작업이 실패하면 속성 페이지의 제목 아래에 요약 오류 메시지가 표시됩니다. 자세한 오류 메시지를 보려면 오류 메시지에 있는 아래쪽 화살표를 클릭하세요.  
  
##  <a name="MoveWGTSQL"></a> Transact-SQL을 사용하여 작업 그룹 이동  
 **Transact-SQL을 사용하여 작업 그룹을 이동하려면**  
  
1.  이동할 작업 그룹 및 이동 대상 리소스 풀의 이름을 지정하여 **ALTER WORKLOAD GROUP** 문을 실행합니다.  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `groupAdhoc` 이라는 작업 그룹을 기본 리소스 풀로 이동합니다.  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [관리](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [리소스 풀 만들기](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [작업 그룹 만들기](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [ALTER WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
