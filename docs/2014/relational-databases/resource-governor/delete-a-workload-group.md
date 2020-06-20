---
title: 작업 그룹 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], delete
- Resource Governor, workload group delete
ms.assetid: d5902c46-5c28-4ac1-8b56-cb4ca2b072d0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 801a731db6c5b31bc479d1a3f6079c45ad9a7c04
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063606"
---
# <a name="delete-a-workload-group"></a>작업 그룹 삭제
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 Transact-SQL을 사용하여 작업 그룹 또는 리소스 풀을 삭제할 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#LimitationsRestrictions), [사용 권한](#Permissions)  
  
-   **작업 그룹을 삭제하려면 다음을 사용합니다.**  [개체 탐색기](#DelWGObjEx), [Resource Governor 속성](#DelWGRGProp) 또는 [Transact-SQL](#DelWGTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
 활성 세션이 들어 있는 작업 그룹은 삭제할 수 없습니다.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 제한 사항  
 작업 그룹에 활성 세션이 있으면 변경 내용을 적용하기 위해 ALTER RESOURCE GOVERNOR RECONFIGURE 문이 호출될 경우 작업 그룹을 삭제하거나 다른 리소스 풀에 이동할 수 없습니다. 다음 동작 중 하나를 수행하여 이 문제를 방지할 수 있습니다.  
  
-   적용된 그룹에서 모든 세션의 연결이 끊어질 때까지 기다린 후 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 다시 실행합니다.  
  
-   KILL 명령을 사용하여 적용된 그룹의 세션을 명시적으로 중지한 후 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 다시 실행합니다. **삭제** 를 사용한 후 활성 세션을 중지하기 전에 세션을 명시적으로 중지하지 않으려는 경우 원래 이름을 사용하여 그룹을 다시 만든 다음 이 그룹을 원래 리소스 풀로 이동합니다.  
  
-   서버를 다시 시작합니다. 다시 시작 프로세스가 완료되면 삭제한 그룹은 생성되지 않고 이동한 그룹은 새 리소스 풀 할당을 사용합니다.  
  
###  <a name="permissions"></a><a name="Permissions"></a> 권한  
 작업 그룹을 삭제하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="delete-a-workload-group-using-object-explorer"></a><a name="DelWGObjEx"></a> 개체 탐색기를 사용하여 작업 그룹 삭제  
 **개체 탐색기를 사용하여 작업 그룹을 삭제하려면**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 풀** 이 나타날 때까지 **관리**노드를 계속 확장합니다.  
  
2.  삭제할 작업 그룹이 포함된 리소스 풀의 **작업 그룹** 노드가 나타날 때까지 **리소스 풀** 을 계속 확장합니다.  
  
3.  작업 그룹을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
4.  **개체 삭제** 창의 **삭제할 개체** 목록에 작업 그룹이 나열됩니다. 작업 그룹을 삭제하려면 **확인**을 클릭합니다.  
  
##  <a name="delete-a-workload-group-using-resource-governor-properties"></a><a name="DelWGRGProp"></a> 리소스 관리자 속성을 사용하여 작업 그룹 삭제  
 **리소스 관리자 속성 페이지를 사용하여 작업 그룹을 삭제하려면**  
  
1.  개체 탐색기에서 **리소스 풀** 이 나타날 때까지 **관리**노드를 계속 확장합니다.  
  
2.  삭제할 작업 그룹이 포함된 리소스 풀을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **리소스 관리자 속성** 페이지가 열립니다.  
  
3.  **리소스 풀의 작업 그룹** 창에서 삭제할 작업 그룹의 줄을 클릭한 다음 줄 왼쪽에 있는 오른쪽 화살표를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
4.  작업 그룹을 삭제하려면 **확인**을 클릭합니다.  
  
##  <a name="delete-a-workload-group-using-transact-sql"></a><a name="DelWGTSQL"></a> Transact-SQL을 사용하여 작업 그룹 삭제  
 **Transact-SQL을 사용하여 작업 그룹을 삭제하려면**  
  
1.  삭제할 작업 그룹의 이름을 지정하여 `DROP WORKLOAD GROUP` 문을 실행합니다.  
  
2.  `ALTER RESOURCE GOVERNOR RECONFIGURE` 문을 실행하기 전에 삭제할 작업 그룹에 활성 요청이 없어야 합니다. 활성 요청이 있으면 `ALTER RESOURCE GOVERNOR`가 실패합니다. 이 문제를 방지하려면 다음 동작 중 하나를 수행하세요.  
  
    -   작업 그룹에서 모든 세션의 연결이 끊어질 때까지 기다립니다.  
  
    -   `KILL` 명령을 사용하여 작업 그룹에 있는 세션을 명시적으로 중지합니다.  
  
    -   서버를 다시 시작합니다. 작업 그룹은 다시 만들어지지 않습니다.  
  
    -   `DROP WORKLOAD GROUP` 문을 실행했지만 변경 내용을 적용하기 위해 세션을 명시적으로 중지하지 않으려는 경우 DROP 문을 실행하기 이전의 이름을 사용하여 그룹을 다시 만든 다음 해당 그룹을 원래 리소스 풀로 이동하십시오.  
  
3.  문을 실행 `ALTER RESOURCE GOVERNOR RECONFIGURE` 합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `groupAdhoc`이라는 작업 그룹을 삭제합니다.  
  
```  
DROP WORKLOAD GROUP groupAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](resource-governor.md)   
 [리소스 풀 만들기](create-a-resource-pool.md)   
 [작업 그룹 만들기](create-a-workload-group.md)   
 [리소스 풀 삭제](delete-a-resource-pool.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-workload-group-transact-sql)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
