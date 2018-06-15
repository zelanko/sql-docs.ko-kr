---
title: 문 매개 변수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e3c7aa5880c80dff412a69d51cda42d24824e01
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913958"
---
# <a name="statement-parameters"></a>문 매개 변수
A *매개 변수* SQL 문에서 변수입니다. 예를 들어 부품 테이블에는 PartID, 설명 및 가격 이라는 열에는 것으로 가정 합니다. 매개 변수 없이 부품을 추가 하려면 필요와 같은 SQL 문을 생성 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 이 문은 새 주문을 삽입, 이지만 하지 주문 입력 응용 프로그램에 적합 한 솔루션 삽입할 값에 응용 프로그램에 하드 코드 수 없기 때문입니다. 대신 삽입할 값을 사용 하 여 런타임 시 SQL 문을 생성 하는 것입니다. 이기도 되지 적합 한 솔루션 생성 문 실행 시의 복잡성 때문입니다. 가장 좋은 방법은의 요소를 대체 하는 **값** 물음표 (?)와 절 또는 *매개 변수 표식을*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 그런 다음 매개 변수 표식이 응용 프로그램 변수에 바인딩됩니다. 새 행을 추가 하려면 응용 프로그램은 하기만 하면 변수 값을 설정 하 고 문을 실행 합니다. 그런 다음 드라이버가 변수의 현재 값을 검색하여 데이터 원본에 보냅니다. 문이 여러 번 실행 수, 하는 경우 응용 프로그램 프로세스가 훨씬 더 효율적으로 만들 수는 문을 준비 하 여 합니다.  
  
 앞서 설명한 문은 새 행을 삽입 하는 주문 입력 응용 프로그램에 하드 코드 수도 있습니다. 그러나 매개 변수 표식을 세로 응용 프로그램에 제한 되지 않습니다. 모든 응용 프로그램에 대 한 텍스트의 변환 하지 않음으로써 런타임 시 SQL 문을 구성의 어려움 쉽게 수행할 합니다. 예를 들어 앞서 설명한 파트 ID는 주로 정수로 응용 프로그램에 저장 합니다. 매개 변수 표식 없이 SQL 문을 생성, 응용 프로그램 파트 ID 텍스트 변환 해야 하 고 데이터 원본으로 변환 해야 하는 정수로 다시 합니다. 매개 변수 마커를 사용 하 여 응용 프로그램은 일반적으로 보낼 수를 정수로 데이터 소스를 정수로 드라이버에 파트 ID를 보낼 수 있습니다. 이렇게 하면 두 가지 변환이 있습니다. 긴 데이터 값에 대 한이 특히 이러한 값의 텍스트 형식을 자주 SQL 문의 허용된 길이 초과 하기 때문에 있습니다.  
  
 매개 변수는 SQL 문에서 특정 위치에만 유효 합니다. Select 목록에 없습니다 허용 예를 들어 (에서 반환할 열 목록이 **선택** 문), 이러한으로 허용 됩니다. 등호 (=)와 같은 이항 연산자의 두 피연산자에 가능한 것 때문에 또는 매개 변수 형식을 결정 합니다. 일반적으로 매개 변수는 데이터 정의 언어 (DDL) 문을 아니라 데이터 조작 언어 (DML) 문을만 유효 합니다. 자세한 내용은 참조 [매개 변수 표식을](../../../odbc/reference/appendixes/parameter-markers.md) 부록 c: SQL 문법에 있습니다.  
  
 SQL 문의 명명 된 매개 변수는 프로시저를 호출 하는 경우 사용할 수 있습니다. 명명 된 매개 변수는 SQL 문에서 아니라 해당 이름으로 식별 됩니다. 호출 하 여 바인딩될 수 **SQLBindParameter**, 있지만 매개 변수가 아닌 IPD (구현 매개 변수 설명자)의 SQL_DESC_NAME 필드에 의해 식별 되는 *ParameterNumber* 의 인수 **SQLBindParameter**합니다. 호출 하 여 바인딩될 수도 **SQLSetDescField** 또는 **SQLSetDescRec**합니다. 명명 된 매개 변수에 대 한 자세한 내용은 참조 [Binding Parameters by Name (Named Parameters)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)이 섹션의 뒷부분에 나오는 합니다. 설명자에 대 한 자세한 내용은 참조 [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 매개 변수](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [매개 변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Long 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [프로시저 매개 변수](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [매개 변수 값 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
