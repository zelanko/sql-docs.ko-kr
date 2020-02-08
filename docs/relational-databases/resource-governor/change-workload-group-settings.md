---
title: 작업 그룹 설정 변경 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], alter
- Resource Governor, workload group alter
ms.assetid: 73b6109c-2ad0-4915-b11b-d40d5a0fdc25
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5389413091f57a5a0dfdad887edad675ee68ff64
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68136928"
---
# <a name="change-workload-group-settings"></a>작업 그룹 설정 변경
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]을 사용하여 작업 그룹 설정을 변경할 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#LimitationsRestrictions), [사용 권한](#Permissions)  
  
-   **작업 그룹에 대한 설정을 변경하려면 다음을 사용합니다.**  [SQL Server Management Studio](#ChgWGProp), [Transact-SQL](#ChgWGTSQL)  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 기본 작업 그룹 및 사용자 정의 작업 그룹의 설정을 변경할 수 있습니다.  
  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 정렬되지 않은 분할된 테이블에서 인덱스 생성에 사용되는 메모리는 관련된 파티션 수에 비례합니다. 필요한 총 메모리가 작업 그룹 설정에서 지정한 쿼리당 제한(REQUEST_MAX_MEMORY_GRANT_PERCENT)을 초과하면 이 인덱스 생성이 실패할 수 있습니다. 기본 작업 그룹에서는 쿼리가 SQL Server 2005 호환성을 유지하며 시작하는 데 필요한 최소 메모리에 대한 쿼리당 제한을 초과할 수 있으므로 기본 리소스 풀에 이러한 쿼리를 실행할 수 있는 총 메모리가 충분히 구성되어 있는 경우 사용자가 기본 작업 그룹에서 동일한 인덱스 생성을 실행할 수 있습니다.  
  
 인덱스를 만들 때 처음에 부여된 것 이상의 메모리 작업 영역을 사용하여 성능을 높일 수 있습니다. 이 특수 처리는 리소스 관리자에서 지원되지만 초기 부여 및 추가 메모리 부여는 작업 그룹 및 리소스 풀 설정에 따라 제한됩니다.  
  
###  <a name="Permissions"></a> 권한  
 작업 그룹 설정을 변경하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="ChgWGProp"></a> SQL Server Management Studio를 사용하여 작업 그룹 설정 변경  
 **다음을 사용하여 작업 그룹 설정을 변경하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  개체 탐색기에서 수정할 작업 그룹이 포함된 **작업 그룹** 폴더가 나타날 때까지 **관리** 노드를 계속 확장합니다.  
  
2.  수정할 작업 그룹을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **리소스 관리자 속성** 페이지의 **리소스 풀의 작업 그룹** 표에서 작업 그룹의 행이 자동으로 선택되어 있지 않으면 선택합니다.  
  
4.  변경할 행의 셀을 클릭 또는 두 번 클릭한 다음 새 값을 입력합니다.  
  
5.  **확인**을 클릭하여 변경 내용을 저장합니다.  
  
##  <a name="ChgWGTSQL"></a> Transact-SQL을 사용하여 작업 그룹 설정 변경  
 **Transact-SQL을 사용하여 작업 그룹 설정을 변경하려면**  
  
1.  변경할 속성 값을 지정하여 ALTER WORKLOAD GROUP 문을 실행합니다.  
  
2.  ALTER RESOURCE GOVERNOR RECONFIGURE 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `groupAdhoc`이라는 작업 그룹에 대한 최대 메모리 부여 비율 설정을 변경합니다.  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
WITH (REQUEST_MAX_MEMORY_GRANT_PERCENT = 30);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [작업 그룹 만들기](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [리소스 풀 만들기](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [리소스 풀 설정 변경](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [ALTER WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
