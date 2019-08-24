---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f3aad1537475e288cff06725b5dbd0fe2383924
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107239"
---
# <a name="statement-parameters"></a>명령문 매개 변수
A *매개 변수* SQL 문에서 변수입니다. 예를 들어 부품 테이블에는 PartID, 설명 및 가격 이라는 열에는 것으로 가정 합니다. 매개 변수 없이 부품을 추가 하는 필요와 같은 SQL 문 생성 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 이 문은 새 주문을 삽입, 이지만 하지 주문 입력 응용 프로그램에 적합 한 솔루션 응용 프로그램에 하드 코드 된 값을 삽입할 수 없기 때문에 있습니다. 대신 삽입할 값을 사용 하 여 런타임 시 SQL 문을 생성 하는 것입니다. 이 아니며 또한 좋은 생성 문 실행 시의 복잡성으로 인해 요소를 대체 하는 가장 적합 한 솔루션을 **값** 물음표 (?)를 사용 하 여 절 또는 *매개 변수 표식을*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 그런 다음 매개 변수 표식이 애플리케이션 변수에 바인딩됩니다. 새 행을 추가할 응용 프로그램에만 변수 값을 설정 하 고 문을 실행 합니다. 그런 다음 드라이버가 변수의 현재 값을 검색하여 데이터 원본에 보냅니다. 문에 여러 번 실행할 수 있으면 응용 프로그램 가능 프로세스가 훨씬 더 효율적으로 문을 준비 하 여 합니다.  
  
 앞서 살펴본 문은 새 행을 삽입 하는 주문 입력 응용 프로그램에 하드 코딩 수 있습니다. 그러나 매개 변수 표식을 세로 응용 프로그램에 제한 되지 않습니다. 응용 프로그램의 경우는 텍스트의 변환 방지 하 여 런타임 시 SQL 문을 생성 하는 것이 어렵기를 간소화할 수 있습니다. 예를 들어 앞서 살펴본 파트 ID는 주로 정수로 응용 프로그램에 저장 합니다. SQL 문의 매개 변수 표식을 없이 생성 되 면 응용 프로그램 파트 ID 텍스트 변환 해야 하 고 데이터 소스의 정수도 다시 변환 해야 합니다. 매개 변수 표식을 사용 하 여 응용 프로그램은 일반적으로 보낼 수는 정수 데이터 원본에는 정수 드라이버 파트 ID를 보낼 수 있습니다. 이렇게 하면 두 변환 합니다. 긴 데이터 값에 대 한 왜냐하면 매우 중요 한 SQL 문의 허용된 길이 자주 초과 하는 이러한 값의 텍스트 서식입니다.  
  
 매개 변수는 SQL 문에서 특정 위치에만 유효 합니다. 예를 들어 이들은 허용 되지 select 목록에 (반환 될 열 목록을 **선택** 문), 이러한으로 허용 됩니다. 등호 (=)와 같은 이항 연산자의 피연산자가 모두 수 것 때문에 매개 변수 형식을 결정 합니다. 일반적으로 매개 변수는 데이터 정의 언어 (DDL) 문 및 데이터 조작 언어 (DML) 문을 에서만 유효 합니다. 자세한 내용은 [매개 변수 표식을](../../../odbc/reference/appendixes/parameter-markers.md) 부록 c: SQL 문법입니다.  
  
 SQL 문의 명명 된 매개 변수, 프로시저를 호출 하는 경우 사용할 수 있습니다. 명명 된 매개 변수는 SQL 문에서 해당 위치가 아닌 이름으로 식별 됩니다. 호출 하 여 바인딩할 수 있습니다 **SQLBindParameter**, 되지만 아닌 매개 변수 IPD (구현 매개 변수 설명자)의 SQL_DESC_NAME 필드에 의해 식별 되는 *상태로* 인수 **SQLBindParameter**합니다. 호출 하 여 바인딩될 수도 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다. 명명 된 매개 변수에 대 한 자세한 내용은 참조 하십시오 [Binding Parameters by Name (Named Parameters)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)이 섹션의 뒷부분에 나오는. 설명자에 대 한 자세한 내용은 참조 하세요. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수 바인딩](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [매개 변수 값 설정](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Long 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [프로시저 매개 변수](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [매개 변수 값 배열](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
