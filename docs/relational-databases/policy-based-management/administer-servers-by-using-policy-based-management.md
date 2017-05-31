---
title: "정책 기반 관리를 사용하여 서버 관리 | Microsoft 문서"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
caps.latest.revision: 76
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bc3d3e94cd6d5993b9647a394338649fe357f021
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="administer-servers-by-using-policy-based-management"></a>정책 기반 관리를 사용하여 서버 관리
   정책 기반 관리는 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 관리하는 정책 기반 시스템입니다. 조건 식을 포함하는 조건을 만들 때 사용합니다. 그런 다음 조건을 데이터베이스 대상 개체에 적용하는 정책을 만듭니다.  

예를 들어 데이터베이스 관리자 권한으로 특정 서버에서 데이터베이스 메일을 사용하도록 설정되지 않도록 서버 옵션을 설정하는 조건과 정책을 만들 수 있습니다. 
   
 > **중요!!** 정책은 일부 기능의 작동 방식에 영향을 줄 수 있습니다. 예를 들어 변경 데이터 캡처 및 트랜잭션 복제는 모두 인덱스가 없는 systranschemas 테이블을 사용합니다. 모든 테이블이 인덱스를 갖도록 하는 정책을 설정하는 경우 이 정책 준수를 강제 적용하면 이러한 기능이 작동하지 않습니다.  
  
 SQL Server management Studio를 사용하여 정책을 만들고 관리하면 다음을 수행할 수 있습니다.
  
1.  구성할 속성을 포함하는 정책 기반 관리 패싯을 선택합니다.  
  
2.  관리 패싯의 상태를 지정하는 조건을 정의합니다.  
  
3.  조건, 대상 집합을 필터링하는 추가 조건 및 평가 모드를 포함하는 정책을 정의합니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 정책을 준수하는지 여부를 확인합니다.  
  
 실패한 정책의 경우 개체 탐색기에서는 개체 탐색기 트리에서 상위 수준에 있는 대상 및 노드 옆에 빨간색 아이콘으로 표시되는 치명적인 상태 경고를 나타냅니다.  
  
> **참고:** 시스템에서 정책에 대한 개체 집합을 계산할 때 기본적으로 시스템 개체가 제외됩니다.  예를 들어, 정책의 개체 집합이 모든 테이블을 참조할 경우 시스템 테이블에 정책이 적용되지 않습니다. 사용자가 시스템 개체에 대해 정책을 평가하려면 개체 집합에 시스템 개체를 명시적으로 추가합니다. 그러나 모든 정책이 **일정 검사** 평가 모드에 대해 지원되더라도 성능상의 이유로 임의 개체 집합의 모든 정책이 **변경 내용 검사** 평가 모드에 대해 지원되지는 않습니다. 자세한 내용은 [http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)를 참조하세요.  
  
## <a name="three-policy-based-management-components"></a>세 가지 정책 기반 관리 구성 요소  
 정책 기반 관리에는 다음과 같은 3가지 구성 요소가 있습니다.  
  
-   정책 관리. 정책 관리자가 정책을 만듭니다.  
  
-   명시적 관리. 관리자가 하나 이상의 관리된 대상을 선택하고 해당 대상이 특정 정책을 준수하는지 여부를 명시적으로 확인하거나 해당 대상이 정책을 준수하도록 명시적으로 지정합니다.  
  
-   평가 모드. 평가 모드에는 4가지 유형이 있으며 이 중 3개는 자동화할 수 있습니다.  
  
    -   **요청 시**. 이 모드는 사용자가 직접 지정한 경우 정책을 평가합니다.  
  
    -   **변경 시: 방지**. 이 자동화된 모드에서는 DDL 트리거를 사용하여 정책 위반을 방지합니다.  
  
        > **중요!** nested triggers 서버 구성 옵션이 해제된 경우에는 **변경 시: 방지** 가 올바르게 작동하지 않습니다. 정책 기반 관리는 DDL 트리거를 사용하여 이 평가 모드를 사용하는 정책을 준수하지 않는 DDL 작업을 검색하고 롤백합니다. 정책 기반 관리 DDL 트리거를 제거하거나 중첩 트리거를 해제하면 이 평가 모드가 제대로 작동하지 않거나 오류가 발생할 수 있습니다.  
  
    -   **변경 시: 로그만**. 이 자동화된 모드에서는 이벤트 알림을 사용하여 관련된 변경이 발생할 때 정책을 평가합니다.  
  
    -   **예약 시**. 이 자동화된 모드에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 사용하여 주기적으로 정책을 평가합니다.  
  
     자동화된 정책이 설정되어 있지 않으면 정책 기반 관리가 시스템 성능에 영향을 주지 않습니다.  
  
## <a name="terms"></a>용어  
 **정책 기반 관리에 의해 관리되는 대상** 
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스, 데이터베이스, 테이블 또는 인덱스와 같이 정책 기반 관리에 의해 관리되는 엔터티입니다. 서버 인스턴스의 모든 대상이 대상 계층을 구성합니다. 대상 집합은 HumanResources 스키마가 소유하는 데이터베이스의 모든 테이블과 같이 대상 필터 집합을 대상 계층에 적용한 결과인 대상 집합입니다.  
  
 **정책 기반 관리 패싯**
 특정 유형의 관리되는 대상에 대한 동작 또는 특징을 모델링하는 논리적 속성 집합입니다. 속성의 수 및 특징은 기본적으로 패싯에 포함되며 패싯 작성자에 의해서만 추가 또는 제거될 수 있습니다. 대상 유형은 하나 이상의 관리 패싯을 구현할 수 있으며 관리 패싯은 하나 이상의 대상 유형에 의해 구현될 수 있습니다. 일부 패싯 속성은 특정 버전에만 적용될 수 있습니다.  
  
 **정책 기반 관리 조건**  
 관리 패싯과 관련하여 정책 기반 관리에 의해 관리되는 대상의 허용되는 상태 집합을 지정하는 부울 식입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 조건을 평가할 때 데이터 정렬을 관측하려고 시도합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬이 Windows 데이터 정렬과 정확하게 일치하지 않을 경우 해당 조건을 테스트하여 알고리즘이 충돌을 어떻게 해결하는지 확인하십시오.  
  
 **정책 기반 관리 정책**  
 평가 모드, 대상 필터 및 일정과 같은 정책 기반 관리 조건 및 예상 동작입니다. 정책은 하나의 조건만 포함할 수 있습니다. 정책은 설정하거나 해제할 수 있습니다. 정책은 msdb 데이터베이스에 저장됩니다.  
  
 **정책 기반 관리 정책 범주**  
 정책 관리에 유용한 사용자 정의 범주입니다. 사용자는 정책을 서로 다른 정책 범주로 분류할 수 있습니다. 정책은 하나의 정책 범주에만 속합니다. 정책 범주는 데이터베이스 및 서버에 적용됩니다. 데이터베이스 수준에서는 다음 조건이 적용됩니다.  
  
-   데이터베이스 소유자는 데이터베이스를 정책 범주 집합에 구독할 수 있습니다.  
  
-   구독한 범주의 정책만 데이터베이스를 제어할 수 있습니다.  
  
-   모든 데이터베이스는 기본 정책 범주에 암시적으로 구독합니다.  
  
 서버 수준에서는 모든 데이터베이스에 정책 범주를 적용할 수 있습니다.  
  
 **실제 정책**  
 대상의 실제 정책은 이 대상을 제어하는 정책입니다. 정책은 다음 조건이 모두 충족되는 경우에만 대상과 관련하여 유효합니다.  
  
-   정책이 설정되어 있습니다.  
  
-   대상이 정책의 대상 집합에 속합니다.  
  
-   대상 또는 대상 상위 항목 중 하나가 이 정책을 포함하는 정책 그룹을 구독합니다.  
  
## <a name="links-to-specific-tasks"></a>특정 작업에 대한 링크 

 - [정책 기반 관리 정책을 저장합니다.](https://msdn.microsoft.com/library/hh213476.aspx)|  
 - [정책 관리자에서 정책 실패를 알리도록 경고 구성](../../relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md)  
 - [새로운 정책 기반 관리 조건 만들기](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) 
 - [정책 기반 관리 조건 삭제](../../relational-databases/policy-based-management/delete-a-policy-based-management-condition.md)
 - [정책 기반 관리 조건의 속성 보기 또는 수정](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
 - [정책 기반 관리 정책 내보내기](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)
 - [정책 기반 관리 정책 가져오기](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)|  
 - [개체의 정책 기반 관리 정책 평가](../../relational-databases/policy-based-management/evaluate-a-policy-based-management-policy-from-an-object.md)
 - [정책 기반 관리 패싯 작업](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)|  
 - [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)

  
 ## <a name="examples"></a>예
 - [Off By Default 정책 만들기](https://msdn.microsoft.com/library/bb500172.aspx)
  - [Off By Default 정책을 실행하도록 서버 구성](https://msdn.microsoft.com/library/bb522470.aspx)
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  

