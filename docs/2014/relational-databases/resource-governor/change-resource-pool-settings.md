---
title: 리소스 풀 설정 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9c81b1c82932fe09a89ffb32f17fd32de34ad8d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183023"
---
# <a name="change-resource-pool-settings"></a>리소스 풀 설정 변경
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 리소스 풀 설정을 변경할 수 있습니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **리소스 풀 설정 변경에 사용되는 도구:**  [SQL Server Management Studio](#ChgRPProp), [Transact-SQL](#ChgRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 최대 CPU 비율은 최소 CPU 비율보다 크거나 같아야 합니다. 최대 메모리 비율은 최소 메모리 비율보다 크거나 같아야 합니다.  
  
 모든 리소스 풀에 대한 최대 CPU 비율과 최소 CPU 비율의 합은 100을 초과할 수 없습니다.  
  
###  <a name="Permissions"></a> Permissions  
 리소스 풀 설정을 변경하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="ChgRPProp"></a> SQL Server Management Studio를 사용하여 리소스 풀 설정 변경  
 **을 사용하여 리소스 풀 설정을 변경하려면(!!) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 풀** 이 나타날 때까지 **관리**노드를 계속 확장합니다.  
  
2.  수정할 리소스 풀을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **리소스 관리자 속성** 페이지의 **리소스 풀** 표에서 리소스 풀의 행이 자동으로 선택되어 있지 않으면 선택합니다.  
  
4.  변경할 행의 셀을 클릭 또는 두 번 클릭한 다음 새 값을 입력합니다.  
  
5.  **확인**을 클릭하여 변경 내용을 저장합니다.  
  
##  <a name="ChgRPTSQL"></a> Transact-SQL을 사용하여 리소스 풀 설정 변경  
 **을 사용하여 리소스 풀 설정을 변경하려면(!!) [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  변경할 속성 값을 지정하여 `ALTER RESOURCE POOL` 문을 실행합니다.  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `poolAdhoc`이라는 리소스 풀에 대한 최대 CPU 비율 설정을 변경합니다.  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [리소스 관리자](resource-governor.md)   
 [리소스 관리자 사용](enable-resource-governor.md)   
 [리소스 풀 만들기](create-a-resource-pool.md)   
 [리소스 풀 삭제](delete-a-resource-pool.md)   
 [리소스 관리자 작업 그룹](resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
