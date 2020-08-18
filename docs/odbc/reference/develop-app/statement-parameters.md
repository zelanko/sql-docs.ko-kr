---
description: 명령문 매개 변수
title: 문 매개 변수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7400367d4b237d2d0e22c6363d1559eb89506d7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482896"
---
# <a name="statement-parameters"></a>명령문 매개 변수
*매개 변수* 는 SQL 문의 변수입니다. 예를 들어 부품 테이블에 PartID, 설명 및 가격 이라는 열이 있다고 가정 합니다. 매개 변수 없이 파트를 추가 하려면 다음과 같은 SQL 문을 생성 해야 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 이 문은 새 주문을 삽입 하지만, 삽입 하는 값은 응용 프로그램에서 하드 코드 될 수 없으므로 주문 입력 응용 프로그램에 적합 한 솔루션이 아닙니다. 다른 방법은 삽입할 값을 사용 하 여 런타임에 SQL 문을 생성 하는 것입니다. 이는 런타임에 문을 생성 하는 복잡성 때문에 좋은 솔루션은 아닙니다. 가장 좋은 해결 방법은 **VALUES** 절의 요소를 물음표 (?) 또는 *매개 변수 표식*으로 바꾸는 것입니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 그런 다음 매개 변수 표식이 애플리케이션 변수에 바인딩됩니다. 새 행을 추가 하기 위해 응용 프로그램은 변수의 값을 설정 하 고 문을 실행 하기만 하면 됩니다. 그런 다음 드라이버가 변수의 현재 값을 검색하여 데이터 원본에 보냅니다. 문이 여러 번 실행 되는 경우 응용 프로그램은 문을 준비 하 여 프로세스를 훨씬 더 효율적으로 만들 수 있습니다.  
  
 표시 된 문은 주문 입력 응용 프로그램에 하드 코딩 되어 새 행을 삽입할 수 있습니다. 그러나 매개 변수 표식은 수직 응용 프로그램으로 제한 되지 않습니다. 응용 프로그램의 경우에는 텍스트로의 변환과 변환을 피하 여 런타임에 SQL 문을 생성 하는 데 어려움이 있습니다. 예를 들어, 앞서 표시 된 파트 ID는 정수로 응용 프로그램에 저장 될 가능성이 높습니다. 매개 변수 표식을 사용 하지 않고 SQL 문을 생성 하는 경우 응용 프로그램은 파트 ID를 텍스트로 변환 하 고 데이터 원본이 다시 정수로 변환 해야 합니다. 응용 프로그램은 매개 변수 표식을 사용 하 여 파트 ID를 정수로 보낼 수 있습니다 .이는 일반적으로 데이터 원본에 정수로 보낼 수 있습니다. 이렇게 하면 두 개의 변환이 저장 됩니다. Long 데이터 값의 경우 이러한 값의 텍스트 형식이 SQL 문의 허용 된 길이를 초과 하는 경우가 많으므로이는 매우 중요 합니다.  
  
 매개 변수는 SQL 문의 특정 위치 에서만 유효 합니다. 예를 들어 select 목록 ( **select** 문에 의해 반환 될 열 목록)은 허용 되지 않으며, 매개 변수 유형을 확인할 수 없기 때문에 등호 (=)와 같은 이항 연산자의 두 피연산자로도 허용 되지 않습니다. 일반적으로 매개 변수는 DML (데이터 조작 언어) 문에서만 유효 하 고 DDL (데이터 정의 언어) 문은 사용할 수 없습니다. 자세한 내용은 부록 C: SQL 문법의 [매개 변수 표식](../../../odbc/reference/appendixes/parameter-markers.md) 을 참조 하세요.  
  
 SQL 문이 프로시저를 호출 하는 경우 명명 된 매개 변수를 사용할 수 있습니다. 명명 된 매개 변수는 SQL 문의 위치가 아니라 이름으로 식별 됩니다. **SQLBindParameter**에 대 한 호출을 통해 바인딩할 수 있지만 매개 변수는 **SQLBindParameter**의 *parameternumber* 인수가 아니라 IPD (구현 매개 변수 설명자)의 SQL_DESC_NAME 필드로 식별 됩니다. **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 바인딩할 수도 있습니다. 명명 된 매개 변수에 대 한 자세한 내용은이 섹션의 뒷부분에 나오는 [이름으로 매개 변수 바인딩 (명명 된 매개 변수)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)을 참조 하세요. 설명자에 대 한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조 하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수 바인딩](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [매개 변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Long 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData에서 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [프로시저 매개 변수](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [매개 변수 값 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
