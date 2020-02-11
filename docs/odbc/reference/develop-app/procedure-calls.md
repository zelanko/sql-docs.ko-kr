---
title: 프로시저 호출 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 926ee91fae207d50248df4c82d1b82bb6424e239
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023249"
---
# <a name="procedure-calls"></a>프로시저 호출
*프로시저* 는 데이터 원본에 저장 된 실행 가능한 개체입니다. 일반적으로 미리 컴파일된 하나 이상의 SQL 문입니다. 프로시저를 호출 하는 이스케이프 시퀀스는 다음과 같습니다.  
  
 **{**[**? =**]**call** *프로시저-name*[**(**[*parameter*] [**,**[*parameter*]] ... **)**]**}**  
  
 여기서 *procedure-name* 은 프로시저의 이름을 지정 하 고 *매개 변수* 는 프로시저 매개 변수를 지정 합니다.  
  
 프로시저 호출 이스케이프 시퀀스에 대 한 자세한 내용은 부록 C: SQL 문법의 [프로시저 호출 이스케이프 시퀀스](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) 를 참조 하세요.  
  
 프로시저는 0개 이상의 매개 변수를 가질 수 있고 구문의 시작 부분에서 선택적 매개 변수 표식 **? =** 로 표시 된 대로 값을 반환할 수도 있습니다. *매개 변수가* 입력 또는 입/출력 매개 변수인 경우 리터럴 또는 매개 변수 표식을 사용할 수 있습니다. 그러나 일부 데이터 소스는 리터럴 매개 변수 값을 허용 하지 않으므로 상호 운용 가능한 응용 프로그램은 항상 매개 변수 표식을 사용 해야 합니다. *매개* 변수가 출력 매개 변수인 경우 매개 변수 표식 이어야 합니다. 프로시저 호출 문이 실행 되기 전에 매개 변수 표식을 **SQLBindParameter** 와 바인딩해야 합니다.  
  
 입력 및 입/출력 매개 변수는 프로시저 호출에서 생략할 수 있습니다. 괄호를 사용 하 여 프로시저를 호출 하지만 {call *procedure-name*()}과 같은 매개 변수를 사용 하지 않는 경우 드라이버는 첫 번째 매개 변수에 기본값을 사용 하도록 데이터 소스에 지시 합니다. 프로시저에 매개 변수가 없으면 프로시저에 오류가 발생할 수 있습니다. {Call *procedure-name*}과 같이 괄호 없이 프로시저를 호출 하는 경우 드라이버는 매개 변수 값을 보내지 않습니다.  
  
 프로시저 호출 시 리터럴을 입력 및 입/출력 매개 변수로 지정할 수 있습니다. 예를 들어 **Insertorder** 프로시저에 입력 매개 변수 5 개가 있다고 가정 합니다. **Insertorder** 에 대 한 다음 호출은 첫 번째 매개 변수를 생략 하 고 두 번째 매개 변수에 대 한 리터럴을 제공 하며 세 번째, 네 번째 및 다섯 번째 매개 변수에 대해 매개 변수 표식을 사용 합니다.  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 매개 변수를 생략 하는 경우 다른 매개 변수에서 구분 하는 쉼표는 계속 표시 되어야 합니다. 입력 또는 입/출력 매개 변수를 생략할 경우 프로시저는 매개 변수의 기본값을 사용합니다. 입력 또는 입/출력 매개 변수의 기본값을 지정 하는 또 다른 방법은 SQL_DEFAULT_PARAM 매개 변수에 바인딩되는 길이/표시기 버퍼의 값을 설정 하는 것입니다.  
  
 입력/출력 매개 변수를 생략 하거나 매개 변수에 대해 리터럴이 제공 되는 경우 드라이버는 출력 값을 삭제 합니다. 마찬가지로 프로시저의 반환 값에 대한 매개 변수 표식을 생략하면 드라이버는 반환 값을 삭제합니다. 마지막으로, 애플리케이션에서 값을 반환하지 않는 프로시저에 대해 반환 값 매개 변수를 지정하면 드라이버는 매개 변수에 바인딩된 길이/표시기 버퍼의 값을 SQL_NULL_DATA로 설정합니다.  
  
 PARTS_IN_ORDERS 프로시저에서 특정 부품 번호가 포함 된 주문 목록이 포함 된 결과 집합을 만드는 경우를 가정 합니다. 다음 코드는 부품 번호 544에 대해이 프로시저를 호출 합니다.  
  
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
  
 데이터 소스가 프로시저를 지원 하는지 여부를 확인 하기 위해 응용 프로그램은 SQL_PROCEDURES 옵션으로 **SQLGetInfo** 를 호출 합니다.  
  
 프로시저에 대 한 자세한 내용은 [절차](../../../odbc/reference/develop-app/procedures-odbc.md)를 참조 하세요.
