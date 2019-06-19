---
title: CHECK 제약 조건 식 대화 상자(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraintexpression
ms.assetid: beb6ce43-3913-4d66-8826-8e885335b790
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0c35a5a617e02eba27e608668117da8856f720d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090777"
---
# <a name="check-constraint-expression-dialog-box-visual-database-tools"></a>CHECK 제약 조건 식 대화 상자(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
CHECK 제약 조건을 테이블이나 열에 연결하려면 SQL 식을 포함해야 합니다. 제공된 입력란에 CHECK 제약 조건 식을 입력합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
식  
식을 입력합니다.  
  
간단한 조건에 대한 데이터를 검사하기 위한 간단한 제약 조건 식을 만들거나 여러 조건에 대한 데이터를 검사하기 위한 복잡한 식을 부울 연산자를 사용하여 만들 수 있습니다. 예를 들어 authors 테이블에 zip 열이 있고, 이 열에 5자리 문자로 구성된 문자열이 필요한 경우를 가정해 볼 수 있습니다. 다음과 같은 제약 조건 식을 사용하면 5자리 수만 사용할 수 있습니다.  
  
```  
zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
```  
  
또는 sales 테이블에 qty라는 열이 있고, 이 열에 0보다 큰 값이 필요한 경우를 가정해 볼 수 있습니다. 다음 예제와 같은 제약 조건을 사용하면 양수 값만 허용되도록 만들 수 있습니다.  
  
```  
qty > 0  
```  
  
또는 orders 테이블에서 모든 신용 카드 주문에 허용되는 신용 카드의 종류를 제한하는 경우를 가정해 볼 수 있습니다. 다음과 같은 제약 조건을 사용하면 신용 카드로 주문하는 경우 Visa, MasterCard 또는 American Express만 허용됩니다.  
  
```  
NOT (payment_method = 'credit card') OR  
   (card_type IN ('VISA', 'MASTERCARD', 'AMERICAN EXPRESS'))  
```  
  
## <a name="to-define-a-constraint-expression"></a>제약 조건 식을 정의하려면  
속성 페이지의 CHECK 제약 조건 탭에서 다음 구문을 사용하여 제약 조건 식 상자에 식을 입력합니다.  
  
<pre>{constant | column_name | function | (subquery)}  
[{operator | AND | OR | NOT}  
{constant | column_name | function | (subquery)}...]</pre>  
  
이 SQL 구문은 다음 매개 변수로 구성되어 있습니다.  
  
|매개 변수|설명|  
|-------------|---------------|  
|constant|숫자 또는 문자 데이터 같은 리터럴 값입니다. 문자 데이터는 작은따옴표(')로 묶어야 합니다.|  
|column_name|열을 지정합니다.|  
|function|기본 제공 함수입니다.|  
|적용한 후|산술 연산자, 비트 연산자, 비교 연산자 또는 문자열 연산자입니다.|  
|AND|두 식을 연결하기 위해 부울 식에 사용됩니다. 두 식이 모두 참인 경우에 결과를 반환합니다.<br /><br />문 하나에 AND와 OR를 모두 사용하는 경우 AND가 먼저 처리됩니다. 계산 순서를 변경하려면 괄호를 사용합니다.|  
|또는|여러 조건을 연결하기 위해 부울 식에 사용됩니다. 한 조건이라도 참이면 결과를 반환합니다.<br /><br />문 하나에 AND와 OR를 모두 사용하는 경우 OR는 AND보다 늦게 처리됩니다. 계산 순서를 변경하려면 괄호를 사용합니다.|  
|NOT|모든 부울 식을 부정합니다. 여기에는 LIKE, NULL, BETWEEN, IN 및 EXISTS 등과 같은 키워드가 포함될 수 있습니다.<br /><br />문 하나에 논리 연산자를 두 개 이상 사용하는 경우 NOT은 제일 먼저 처리됩니다. 계산 순서를 변경하려면 괄호를 사용합니다.|  
  
## <a name="see-also"></a>참고 항목  
[UNIQUE 제약 조건 및 CHECK 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md)  
[UNIQUE 제약 조건 만들기](../../relational-databases/tables/create-unique-constraints.md)  
  
