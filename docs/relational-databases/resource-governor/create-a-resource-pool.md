---
title: 리소스 풀 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 93add4b3d9ed4ff71a57845443813c323861145b
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53379680"
---
# <a name="create-a-resource-pool"></a>리소스 풀 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 리소스 풀을 만들 수 있습니다. 리소스 풀의 보안 주체를 이해하려면 [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)을(를) 참조하세요.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#LimitationsRestrictions), [사용 권한](#Permissions)  
  
-   **리소스 풀을 만들려면 다음을 사용합니다.**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 최대 CPU 비율은 최소 CPU 비율보다 크거나 같아야 합니다. 최대 메모리 비율은 최소 메모리 비율보다 크거나 같아야 합니다.  
  
 모든 리소스 풀에 대한 최대 CPU 비율과 최소 CPU 비율의 합은 100을 초과할 수 없습니다.  
  
###  <a name="Permissions"></a> Permissions  
 리소스 풀을 만들려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="CreRPProp"></a> SQL Server Management Studio를 사용하여 리소스 풀 만들기  
 **다음을 사용하여 리소스 풀 만들기: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 가 나타날 때까지 **관리**노드를 계속 확장합니다.  
  
2.  **Resource Governor**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **리소스 풀** 표에서 빈 행의 첫 번째 열을 클릭합니다. 이 열에는 별표(*)가 표시되어 있습니다.  
  
4.  **이름** 열의 빈 셀을 두 번 클릭합니다. 리소스 풀에 사용할 이름을 입력합니다.  
  
5.  변경할 행의 다른 셀을 클릭 또는 두 번 클릭한 다음 새 값을 입력합니다.  
  
6.  **확인**을 클릭하여 변경 내용을 저장합니다.  
  
##  <a name="CreRPTSQL"></a> Transact-SQL을 사용하여 리소스 풀 만들기  
 **다음을 사용하여 리소스 풀 만들기: [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  설정할 속성 값을 지정하여 [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) 또는 [CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 문을 실행합니다.  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** 문을 실행합니다.  
  
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
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 풀 설정 변경](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [리소스 풀 삭제](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [템플릿을 사용하여 리소스 관리자 구성](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
