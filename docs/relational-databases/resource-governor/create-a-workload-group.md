---
title: 작업 그룹 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
ms.assetid: 072868ec-ceff-4db6-941b-281af731a067
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: f09c3fecff6dd64934a456fafc0eabfcb134c30f
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581827"
---
# <a name="create-a-workload-group"></a>작업 그룹 만들기
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 작업 그룹을 만들 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#LimitationsRestrictions), [사용 권한](#Permissions)  
  
-   **작업 그룹을 만들려면 다음을 사용합니다.**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 정렬되지 않은 분할된 테이블에서 인덱스 생성에 사용되는 메모리는 관련된 파티션 수에 비례합니다. 필요한 총 메모리가 작업 그룹 설정에서 지정한 쿼리당 제한(REQUEST_MAX_MEMORY_GRANT_PERCENT)을 초과하면 이 인덱스 생성이 실패할 수 있습니다. 기본 작업 그룹에서는 쿼리가 SQL Server 2005 호환성을 유지하며 시작하는 데 필요한 최소 메모리에 대한 쿼리당 제한을 초과할 수 있으므로 기본 리소스 풀에 이러한 쿼리를 실행할 수 있는 총 메모리가 충분히 구성되어 있는 경우 사용자가 기본 작업 그룹에서 동일한 인덱스 생성을 실행할 수 있습니다.  
  
 인덱스를 만들 때 처음에 부여된 것 이상의 메모리 작업 영역을 사용하여 성능을 높일 수 있습니다. 이 특수 처리는 리소스 관리자에서 지원되지만 초기 부여 및 추가 메모리 부여는 작업 그룹 및 리소스 풀 설정에 따라 제한됩니다.  
  
###  <a name="Permissions"></a> 사용 권한  
 작업 그룹을 만들려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="CreRPProp"></a> SQL Server Management Studio를 사용하여 작업 그룹 만들기  
 **다음을 사용하여 작업 그룹을 만들기: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  개체 탐색기에서 수정할 작업 그룹이 포함된 리소스 풀이 나타날 때까지 **관리** 노드를 계속 확장합니다.  
  
2.  **Workload Groups** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 작업 그룹**을 클릭합니다.  
  
3.  **리소스 풀** 표에 작업 그룹을 추가하려는 리소스 풀이 강조 표시되었는지 확인합니다.  
  
4.  **리소스 풀의 작업 그룹** 표에 빈 이름이 포함된 새 줄이 나타나고 다른 열에는 기본 값이 표시됩니다.  
  
5.  **이름** 셀을 클릭하고 작업 그룹의 이름을 입력합니다.  
  
6.  기본 설정에서 변경하려는 행의 다른 셀을 클릭 또는 두 번 클릭한 다음 새 값을 입력합니다.  
  
7.  **확인**을 클릭하여 변경 내용을 저장합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="CreRPTSQL"></a> Transact-SQL을 사용하여 작업 그룹 만들기  
 **다음을 사용하여 작업 그룹을 만들기: [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  설정할 속성 값을 지정하여 CREATE WORKLOAD GROUP 문을 실행합니다.  
  
2.  ALTER RESOURCE GOVERNOR RECONFIGURE 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `groupAdhoc` 이라는 리소스 풀에 있는 `poolAdhoc`이라는 작업 그룹을 만듭니다.  
  
```  
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [리소스 풀 만들기](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [작업 그룹 설정 변경](../../relational-databases/resource-governor/change-workload-group-settings.md)   
 [분류자 사용자 정의 함수 만들기 및 테스트](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
  
