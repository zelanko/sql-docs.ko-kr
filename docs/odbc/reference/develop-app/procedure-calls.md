---
title: 수속 전화 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9c52e72512c8b81c6872461207f235ea2731ac5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282233"
---
# <a name="procedure-calls"></a>프로시저 호출
*프로시저는* 데이터 원본에 저장된 실행 가능한 개체입니다. 일반적으로 미리 컴파일된 하나 이상의 SQL 문입니다. 프로시저를 호출하기 위한 이스케이프 시퀀스는  
  
 **{**[**?=**]**호출** *프로시저 이름*[**[ [**[ 매개*변수*]**[ [** 매개*변수*]... **)**]**}**  
  
 여기서 *프로시저 이름은* 프로시저 이름을 지정하고 *매개 변수는* 프로시저 매개 변수를 지정합니다.  
  
 프로시저 호출 이스케이프 시퀀스에 대한 자세한 내용은 부록 C: SQL 문법의 [프로시저 호출 이스케이프 시퀀스를](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) 참조하십시오.  
  
 프로시저는 0개 이상의 매개 변수를 가질 수 있고 또한 구문이 시작될 때 선택적 매개 변수 마커 **?=로** 표시된 값을 반환할 수도 있습니다. *매개 변수가* 입력 또는 입력/출력 매개변수인 경우 리터럴 또는 매개 변수 마커일 수 있습니다. 그러나 상호 운용 가능한 응용 프로그램은 일부 데이터 원본이 리터럴 매개 변수 값을 허용하지 않으므로 항상 매개 변수 마커를 사용해야 합니다. *매개 변수가* 출력 매개 변수인 경우 매개 변수 마커여야 합니다. 프로시저 호출 문이 실행되기 전에 매개 변수 마커는 **SQLBindParameter와** 바인딩되어야 합니다.  
  
 입력 및 입/출력 매개 변수는 프로시저 호출에서 생략할 수 있습니다. 프로시저가 괄호로 호출되지만 {call *프로시저*이름()}과 같은 매개 변수가 없는 경우 드라이버는 데이터 원본에 첫 번째 매개 변수에 대한 기본값을 사용하도록 지시합니다. 프로시저에 매개 변수가 없는 경우 프로시저가 실패할 수 있습니다. {call *프로시저 이름*}과 같은 괄호 없이 프로시저를 호출하는 경우 드라이버는 매개 변수 값을 보내지 않습니다.  
  
 프로시저 호출 시 리터럴을 입력 및 입/출력 매개 변수로 지정할 수 있습니다. 예를 들어 **프로시저 InsertOrder에** 5개의 입력 매개 변수가 있다고 가정합니다. **InsertOrder에** 대한 다음 호출은 첫 번째 매개 변수를 생략하고 두 번째 매개 변수에 대한 리터럴을 제공하며 세 번째, 네 번째 및 다섯 번째 매개 변수에 대한 매개 변수 마커를 사용합니다.  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 매개 변수를 생략하는 경우 다른 매개 변수에서 매개 변수를 구분하는 쉼표가 계속 나타나야 합니다. 입력 또는 입/출력 매개 변수를 생략할 경우 프로시저는 매개 변수의 기본값을 사용합니다. 입력 또는 입력/출력 매개 변수의 기본값을 지정하는 또 다른 방법은 SQL_DEFAULT_PARAM 위해 매개 변수에 바인딩된 길이/표시기 버퍼의 값을 설정하는 것입니다.  
  
 입력/출력 매개 변수를 생략하거나 매개 변수에 대해 리터럴이 제공된 경우 드라이버는 출력 값을 삭제합니다. 마찬가지로 프로시저의 반환 값에 대한 매개 변수 표식을 생략하면 드라이버는 반환 값을 삭제합니다. 마지막으로, 애플리케이션에서 값을 반환하지 않는 프로시저에 대해 반환 값 매개 변수를 지정하면 드라이버는 매개 변수에 바인딩된 길이/표시기 버퍼의 값을 SQL_NULL_DATA로 설정합니다.  
  
 프로시저 PARTS_IN_ORDERS 특정 부품 번호가 포함된 주문 목록을 포함하는 결과 집합을 만든다고 가정합니다. 다음 코드는 부품 번호 544에 대해 이 프로시저를 호출합니다.  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 데이터 원본이 프로시저를 지원하는지 여부를 확인하기 위해 응용 프로그램은 SQL_PROCEDURES 옵션을 사용하여 **SQLGetInfo를** 호출합니다.  
  
 절차에 대한 자세한 내용은 [프로시저 을](../../../odbc/reference/develop-app/procedures-odbc.md)참조하십시오.
