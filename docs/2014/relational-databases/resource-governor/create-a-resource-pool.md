---
title: 리소스 풀 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f4d18ef352c3e5ab6342e573d16bc3deaed5db72
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211997"
---
# <a name="create-a-resource-pool"></a>리소스 풀 만들기
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 리소스 풀을 만들 수 있습니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To create a resource pool, using:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 제한 사항  
 최대 CPU 비율은 최소 CPU 비율보다 크거나 같아야 합니다. 최대 메모리 비율은 최소 메모리 비율보다 크거나 같아야 합니다.  
  
 모든 리소스 풀에 대한 최대 CPU 비율과 최소 CPU 비율의 합은 100을 초과할 수 없습니다.  
  
###  <a name="permissions"></a><a name="Permissions"></a> 권한  
 리소스 풀을 만들려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="create-a-resource-pool-using-sql-server-management-studio"></a><a name="CreRPProp"></a> SQL Server Management Studio를 사용하여 리소스 풀 만들기  
 **다음을 사용하여 리소스 풀 만들기: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 가 나타날 때까지 **관리**노드를 계속 확장합니다.  
  
2.  **Resource Governor**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **리소스 풀** 표에서 빈 행의 첫 번째 열을 클릭합니다. 이 열에는 별표(*)가 표시되어 있습니다.  
  
4.  **이름** 열의 빈 셀을 두 번 클릭합니다. 리소스 풀에 사용할 이름을 입력합니다.  
  
5.  변경할 행의 다른 셀을 클릭 또는 두 번 클릭한 다음 새 값을 입력합니다.  
  
6.  **확인**을 클릭하여 변경 내용을 저장합니다.  
  
##  <a name="create-a-resource-pool-using-transact-sql"></a><a name="CreRPTSQL"></a>Transact-sql을 사용 하 여 리소스 풀 만들기  
 **다음을 사용하여 리소스 풀 만들기: [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  설정할 속성 값을 지정하여 `CREATE RESOURCE POOL` 문을 실행합니다.  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** 문을 실행 합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `poolAdhoc`이라는 리소스 풀을 만듭니다.  
  
```  
CREATE RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 20);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Resource Governor](resource-governor.md)   
 [Resource Governor 사용](enable-resource-governor.md)   
 [Resource Governor 리소스 풀](resource-governor-resource-pool.md)   
 [리소스 풀 설정 변경](change-resource-pool-settings.md)   
 [리소스 풀 삭제](delete-a-resource-pool.md)   
 [템플릿을 사용 하 여 Resource Governor 구성](configure-resource-governor-using-a-template.md)   
 [작업 그룹 Resource Governor](resource-governor-workload-group.md)   
 [Resource Governor 분류자 함수](resource-governor-classifier-function.md)   
 [Transact-sql&#41;&#40;리소스 풀 만들기](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
