---
title: 리소스 관리자 사용 안 함 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, disabling
ms.assetid: 2c2d2db0-34a5-4f50-b783-17693e3ce3f1
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: eadaffc01ea26da4c707c031ca6d9b3f3e30e113
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="disable-resource-governor"></a>리소스 관리자 사용 안 함
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 Transact-SQL을 사용하여 리소스 관리자를 사용하지 않도록 설정할 수 있습니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **Resource Governor를 사용하지 않도록 설정하는 데 사용되는 도구:**  [개체 탐색기](#RGOffObjEx), [Resource Governor 속성](#RGOffProp), [Transact-SQL](#RGOffTSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 리소스 관리자를 사용하지 않도록 설정하면 다음과 같은 결과가 나타납니다.  
  
-   분류자 함수가 실행되지 않습니다.  
  
-   모든 새 연결이 자동으로 기본 작업 그룹으로 분류됩니다.  
  
-   시스템에서 시작한 요청이 내부 작업 그룹으로 분류됩니다.  
  
-   기존의 모든 작업 그룹 및 리소스 풀 설정이 해당 기본값으로 다시 설정됩니다. 이 경우 제한에 도달해도 이벤트가 발생하지 않습니다.  
  
-   정상적인 시스템 모니터링은 영향을 받지 않습니다.  
  
-   구성을 변경할 수 있지만 리소스 관리자를 사용하도록 설정할 때까지 변경 내용이 적용되지 않습니다.  
  
-   SQL Server를 다시 시작하면 리소스 관리자가 구성을 로드하지 않고 기본 및 내부 작업 그룹과 리소스 풀만 사용합니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 사용자 트랜잭션에 있을 때에는 **ALTER RESOURCE GOVERNOR** 문을 사용하여 리소스 관리자를 사용하지 않도록 설정할 수 없습니다.  
  
###  <a name="Permissions"></a> Permissions  
 리소스 관리자를 사용하지 않도록 설정하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="RGOffObjEx"></a> 개체 탐색기를 사용하여 리소스 관리자를 사용하지 않도록 설정  
 **개체 탐색기를 사용하여 리소스 관리자를 사용하지 않도록 설정하려면**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 까지 **관리**노드를 계속 확장합니다.  
  
2.  **Resource Governor**를 마우스 오른쪽 단추로 클릭한 다음 **사용 안 함**을 클릭합니다.  
  
##  <a name="RGOffProp"></a> 리소스 관리자 속성을 사용하여 리소스 관리자를 사용하지 않도록 설정  
 **리소스 관리자 속성 페이지를 사용하여 리소스 관리자를 사용하지 않도록 설정하려면**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 까지 **관리**노드를 계속 확장합니다.  
  
2.  **리소스 관리자** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 그러면 **리소스 관리자 속성** 페이지가 열립니다.  
  
3.  **리소스 관리자 사용** 확인란을 클릭해서 상자를 선택 해제한 다음 **확인**을 클릭합니다.  
  
##  <a name="RGOffTSQL"></a> Transact-SQL을 사용하여 리소스 관리자를 사용하지 않도록 설정  
 **Transact-SQL을 사용하여 리소스 관리자를 사용하지 않도록 설정**  
  
1.  **ALTER RESOURCE GOVERNOR DISABLE** 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 리소스 관리자를 사용하도록 설정합니다.  
  
```  
ALTER RESOURCE GOVERNOR DISABLE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [관리](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
