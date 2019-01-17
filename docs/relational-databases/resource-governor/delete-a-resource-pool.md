---
title: 리소스 풀 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool delete
- resource pools [SQL Server], delete
ms.assetid: 3bdd348b-6582-4ffa-80ef-d49e50596ce5
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 8e95c665cc96d98de6664e5af58ed90d4cf70d02
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380564"
---
# <a name="delete-a-resource-pool"></a>리소스 풀 삭제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 Transact-SQL을 사용하여 리소스 풀을 삭제할 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#LimitationsRestrictions), [사용 권한](#Permissions)  
  
-   **리소스 풀을 삭제하려면 다음을 사용합니다.** [SQL Server Management Studio](#DelRPSSMS), [Transact-SQL](#DelRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
 작업 그룹이 들어 있는 리소스 풀은 삭제할 수 없습니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 리소스 관리자 기본 풀 또는 내부 리소스 풀을 삭제할 수 없습니다. 작업 그룹이 들어 있는 리소스 풀은 삭제할 수 없습니다. 자세한 내용은 [Delete a Workload Group](../../relational-databases/resource-governor/delete-a-workload-group.md)을 참조하세요.  
  
###  <a name="Permissions"></a> Permissions  
 리소스 풀을 삭제하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="DelRPSSMS"></a> 개체 탐색기를 사용하여 리소스 풀 삭제  
 **SQL Server Management Studio를 사용하여 리소스 풀을 삭제하려면**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 가 나타날 때까지 **관리**노드를 계속 확장합니다.  
  
2.  삭제할 리소스 풀을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
3.  **개체 삭제** 창의 **삭제할 개체** 목록에 리소스 풀이 나열됩니다. 리소스 풀을 삭제하려면 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  삭제하려고 하는 리소스 풀에 작업 그룹이 들어 있으면 해당 리소스 풀을 삭제할 수 없습니다.  
  
##  <a name="DelRPTSQL"></a> Transact-SQL을 사용하여 리소스 풀 삭제  
 **Transact-SQL을 사용하여 리소스 풀을 삭제하려면**  
  
1.  삭제할 리소스의 이름을 지정하는 **DROP RESOURCE POOL** 또는 **DROP EXTERNAL RESOURCE POOL** 문을 실행합니다.  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `poolAdhoc`이라는 작업 그룹을 삭제합니다.  
  
```  
DROP RESOURCE POOL poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 풀 만들기](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [리소스 풀 설정 변경](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [DROP WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
