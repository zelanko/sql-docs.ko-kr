---
title: 새 조건 만들기 또는 조건 열기 대화 상자, 일반 페이지 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de374ce97cd1d2cfe1f5ca9967439e705a47b255
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32953438"
---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>새 조건 만들기 또는 조건 열기 대화 상자, 일반 페이지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 대화 상자를 사용하여 정책 기반 관리 조건을 만들거나 변경할 수 있습니다. 조건은 패싯과 관련하여 정책 기반 관리로 관리되는 대상의 허용되는 상태 집합을 지정하는 부울 식입니다. **식/필드** 상자에서 선택할 수 있는 속성은 사용되는 패싯에 따라 달라집니다. 조건과 패싯 및 정책 간의 관계는 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)를 참조하세요.  
  
## <a name="options"></a>변수  
 **이름**  
 새 조건의 경우 새 조건 이름을 입력합니다. 기존 조건의 경우 이름이 표시됩니다.  
  
 **패싯**  
 이 조건에 사용되는 패싯입니다.  
  
 **AndOr**  
 여러 식을 추가할 경우 식을 **And** 를 사용하여 조인할지, 아니면 **Or**를 사용하여 조인할지를 나타냅니다. 식이 하나만 있는 경우에는 비어 있습니다.  
  
 **필드**  
 각 패싯은 설정할 수 있는 하나 이상의 속성을 표시합니다. 필드 상자에서 사용 가능한 속성 목록에 있는 속성을 선택하여 이 조건에 대한 식을 만듭니다.  
  
 **연산자**  
 이 식에 대한 비교 연산자를 선택합니다. 연산자는 =, !=, >, >=, <, <=, [NOT]LIKE, [NOT]IN과 같습니다. 일부 속성에서는 모든 연산자를 사용하지 못할 수 있습니다.  
  
 **Value**  
 이 식에 대한 값 설정입니다. 허용되는 값은 패싯에 따라 달라집니다. 값은 TRUE/FALSE, 문자열 또는 숫자일 수 있습니다. 문자열 값은 작은따옴표로 묶어야 합니다(예: **'AdventureWorks'**). 일부 속성에서는 모든 연산자를 사용하지 못할 수 있습니다.  
  
## <a name="group-clauses"></a>절 그룹화  
 절을 그룹화하여 나머지 쿼리와 분리된 하나의 단위로 해당 절을 실행할 수 있습니다. 이는 수식이나 논리 문에서 식을 괄호로 묶는 것과 같습니다. 절 그룹화는 복잡한 쿼리를 작성할 때 유용합니다.  
  
 **절을 그룹화하려면**  
  
-   Shift 또는 Ctrl 키를 누른 다음 두 개 이상의 절을 클릭하여 범위를 선택합니다. 선택한 영역을 마우스 오른쪽 단추로 클릭한 다음 **절 그룹화**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
