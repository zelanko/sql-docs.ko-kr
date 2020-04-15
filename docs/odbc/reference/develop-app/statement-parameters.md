---
title: 문 매개 변수 | 마이크로 소프트 문서
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
ms.openlocfilehash: 02327ff4bb6a1ac3ac57fbf7d3c6b09b70c11534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306824"
---
# <a name="statement-parameters"></a>명령문 매개 변수
*매개 변수는* SQL 문의 변수입니다. 예를 들어 부품 테이블에 PartID, 설명 및 가격이라는 열이 있다고 가정합니다. 매개 변수가 없는 부품을 추가하려면 다음과 같은 SQL 문을 생성해야 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 이 문은 새 순서를 삽입하지만 삽입할 값을 응용 프로그램에서 하드 코딩할 수 없기 때문에 주문 입력 응용 프로그램에는 좋은 솔루션이 아닙니다. 다른 방법은 삽입할 값을 사용하여 런타임에 SQL 문을 생성하는 것입니다. 런타임에 문을 생성하는 것이 복잡하기 때문에 이 솔루션도 좋은 해결책이 아닙니다. 가장 좋은 해결책은 **VALUE** 절의 요소를 물음표(?) 또는 *매개 변수 마커로*바꾸는 것입니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 그런 다음 매개 변수 표식이 애플리케이션 변수에 바인딩됩니다. 새 행을 추가하려면 응용 프로그램은 변수의 값을 설정하고 문을 실행하기만 하면 됩니다. 그런 다음 드라이버가 변수의 현재 값을 검색하여 데이터 원본에 보냅니다. 명령문이 여러 번 실행되는 경우 응용 프로그램은 문을 준비하여 프로세스를 더욱 효율적으로 만들 수 있습니다.  
  
 방금 표시된 문은 새 행을 삽입하기 위한 주문 입력 응용 프로그램에서 하드 코딩될 수 있습니다. 그러나 매개 변수 마커는 수직 응용 프로그램에만 국한되지 않습니다. 모든 응용 프로그램의 경우 텍스트로의 변환을 방지하여 런타임에 SQL 문을 생성하는 어려움을 쉽게 할 수 있습니다. 예를 들어 방금 표시된 부품 ID는 응용 프로그램에 정수로 저장될 가능성이 높습니다. SQL 문이 매개 변수 마커 없이 생성되는 경우 응용 프로그램은 부품 ID를 텍스트로 변환해야 하며 데이터 원본은 이를 정수로 다시 변환해야 합니다. 매개 변수 마커를 사용 하 여 응용 프로그램은 일반적으로 정수로 데이터 원본에 보낼 수 있는 정수로 드라이버에 부품 ID를 보낼 수 있습니다. 이렇게 하면 두 개의 변환이 저장됩니다. 긴 데이터 값의 경우 이러한 값의 텍스트 형식이 SQL 문의 허용 길이를 초과하는 경우가 많기 때문에 매우 중요합니다.  
  
 매개 변수는 SQL 문의 특정 위치에서만 유효합니다. 예를 들어 선택 **목록(SELECT** 문으로 반환할 열 목록)에서 허용되지 않으며 매개 변수 형식을 확인할 수 없기 때문에 등호(=)와 같은 이진 연산자의 두 피연산자로 허용되지 않습니다. 일반적으로 매개 변수는 DML(데이터 조작 언어) 명령문이 아니라 DDL(데이터 정의 언어) 문에서만 유효합니다. 자세한 내용은 부록 C: SQL 문법의 [매개 변수 마커를](../../../odbc/reference/appendixes/parameter-markers.md) 참조하십시오.  
  
 SQL 문이 프로시저를 호출할 때 명명된 매개 변수를 사용할 수 있습니다. 명명된 매개 변수는 SQL 문의 위치가 아니라 이름으로 식별됩니다. **SQLBindParameter에**대한 호출로 바인딩할 수 있지만 매개 변수는 매개 변수가 아닌 IPD의 SQL_DESC_NAME 필드(구현 매개 변수 설명자)로 *식별되며, 매개 변수는 PARAMETERNumber* 인수가 아니라 **SQLBindParameter**. SQLSetDescField 또는 **SQLSetDescRec를**호출하여 바인딩할 수도 있습니다. **SQLSetDescField** 명명된 매개 변수에 대한 자세한 내용은 이 섹션의 다음 부분의 [이름(명명된 매개 변수)별로 매개 변수 바인딩을](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)참조하십시오. 설명자에 대한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수 바인딩](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [매개 변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Long 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData에 의한 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [프로시저 매개 변수](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [매개 변수 값 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
