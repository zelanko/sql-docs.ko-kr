---
title: 리소스 관리자 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, enabling
ms.assetid: 4d17af53-cf11-4ce4-aab4-deda94a49836
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d69214acdfc469a9c74afbd1ec9c379acc02689
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617831"
---
# <a name="enable-resource-governor"></a>리소스 관리자 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  리소스 관리자는 기본적으로 해제되어 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 Transact-SQL을 사용하여 리소스 관리자를 사용하도록 설정할 수 있습니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **Resource Governor를 사용하도록 설정하는 데 사용되는 도구:**  [개체 탐색기](#RGOnObjEx), [Resource Governor 속성](#RGOnProp), [Transact-SQL](#RGOnTSQL)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 리소스 관리자를 사용하도록 설정하면 다음과 같은 결과가 나타납니다.  
  
-   작업 그룹에 해당 작업을 할당할 수 있도록 새 연결에 대해 분류자 함수가 실행됩니다.  
  
-   리소스 관리자 구성에 지정된 리소스 제한이 강제로 적용됩니다.  
  
-   리소스 관리자를 사용하도록 설정하기 전부터 있었던 요청은 리소스 관리자를 사용하지 않도록 설정했을 때 변경한 구성에 의해 영향을 받습니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 사용자 트랜잭션에 있을 때에는 **ALTER RESOURCE GOVERNOR** 문을 사용하여 리소스 관리자를 사용하도록 설정할 수 없습니다.  
  
###  <a name="Permissions"></a> Permissions  
 리소스 관리자를 사용하도록 설정하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="RGOnObjEx"></a> 개체 탐색기를 사용하여 리소스 관리자를 사용하도록 설정  
 **개체 탐색기를 사용하여 리소스 관리자를 사용하도록 설정하려면**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 까지 **관리**노드를 계속 확장합니다.  
  
2.  **Resource Governor**를 마우스 오른쪽 단추로 클릭한 다음 **사용**을 클릭합니다.  
  
##  <a name="RGOnProp"></a> 리소스 관리자 속성을 사용하여 리소스 관리자를 사용하도록 설정  
 **리소스 관리자 속성 페이지를 사용하여 리소스 관리자를 사용하도록 설정하려면**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 관리자** 까지 **관리**노드를 계속 확장합니다.  
  
2.  **리소스 관리자** 를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 그러면 **리소스 관리자 속성** 페이지가 열립니다.  
  
3.  **리소스 관리자 사용** 확인란을 클릭한 다음 **확인**을 클릭합니다.  
  
##  <a name="RGOnTSQL"></a> Transact-SQL을 사용하여 리소스 관리자를 사용하도록 설정  
 **Transact-SQL을 사용하여 리소스 관리자를 사용하도록 설정**  
  
1.  **ALTER RESOURCE GOVERNOR RECONFIGURE** 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 리소스 관리자를 사용하도록 설정합니다.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [관리](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용 안 함](../../relational-databases/resource-governor/disable-resource-governor.md)   
 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
