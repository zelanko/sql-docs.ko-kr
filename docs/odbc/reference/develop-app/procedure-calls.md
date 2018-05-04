---
title: 프로시저 호출 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cdcf2922260d834bf4da104cae82c49ffb77f257
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="procedure-calls"></a>프로시저 호출
A *프로시저* 는 데이터 원본에 저장 된 실행 개체입니다. 일반적으로 미리 컴파일된 하나 이상의 SQL 문입니다. 프로시저 호출에 대 한 이스케이프 시퀀스는  
  
 **{**[**? =**]**호출** *프로시저 이름*[**(**[*매개 변수*] [**,**[*매개 변수*]]... **)**]**}**  
  
 여기서 *프로시저 이름* 프로시저의 이름을 지정 하 고 *매개 변수* 프로시저 매개 변수를 지정 합니다.  
  
 프로시저 호출 이스케이프 시퀀스에 대 한 자세한 내용은 참조 [프로시저 Call 이스케이프 시퀀스](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) 부록 c: SQL 문법에 있습니다.  
  
 프로시저는 0개 이상의 매개 변수를 가질 수 있고 선택적 매개 변수 표식으로 표시 된 대로 값을 반환할 수도 있습니다 **? =** 구문의 시작 부분에 있습니다. 경우 *매개 변수* 입력 또는 입/출력 매개 변수를 리터럴 또는 매개 변수 표식을 사용할 수 있습니다. 그러나 상호 운용 가능한 응용 프로그램 일부 데이터 원본의 리터럴 매개 변수 값을 허용 하지 않는 항상 매개 변수 표식을 사용 해야 합니다. 경우 *매개 변수* 는 출력 매개 변수는 매개 변수 표식을 이어야 합니다. 매개 변수 표식에 바인딩되어야 **SQLBindParameter** 프로시저 호출 하기 전에 문이 실행 됩니다.  
  
 입력 및 입/출력 매개 변수는 프로시저 호출에서 생략할 수 있습니다. 경우 프로시저 호출 매개 변수를 제외 괄호 함께 같은 {호출 *프로시저 이름*()을 (를), 드라이버는 첫 번째 매개 변수에 대 한 기본값을 사용 하는 데이터 원본의 지시 합니다. 프로시저에 매개 변수가이 실패 하는 절차를 발생할 수 있습니다. 프로시저와 같은 괄호 없이 호출 됩니다 {호출 *프로시저 이름*}, 드라이버는 모든 매개 변수 값을 전송 하지 않습니다.  
  
 프로시저 호출 시 리터럴을 입력 및 입/출력 매개 변수로 지정할 수 있습니다. 예를 들어 프로시저 **InsertOrder** 에 5 개의 입력 매개 변수가 있습니다. 다음에 대 한 호출 **InsertOrder** 첫 번째 매개 변수를 생략 하 고, 두 번째 매개 변수에 대 한 리터럴을 제공, 세 번째, 네 번째 및 다섯 번째에 대 한 매개 변수 표식을 사용 하 여 매개 변수:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 매개 변수를 생략 하면 다른 매개 변수에서 구분 하는 쉼표 해야 여전히 나타나는지 확인 합니다. 입력 또는 입/출력 매개 변수를 생략할 경우 프로시저는 매개 변수의 기본값을 사용합니다. SQL_DEFAULT_PARAM으로 매개 변수에 바인딩된 길이/표시기 버퍼의 값을 설정 하는 입력 또는 입/출력 매개 변수의 기본값을 지정 하는 다른 방법은 합니다.  
  
 입력/출력 매개 변수를 생략 하거나 리터럴을 매개 변수에 대해 제공 하는 경우 드라이버는 출력 값을 삭제 합니다. 마찬가지로 프로시저의 반환 값에 대한 매개 변수 표식을 생략하면 드라이버는 반환 값을 삭제합니다. 마지막으로, 응용 프로그램에서 값을 반환하지 않는 프로시저에 대해 반환 값 매개 변수를 지정하면 드라이버는 매개 변수에 바인딩된 길이/표시기 버퍼의 값을 SQL_NULL_DATA로 설정합니다.  
  
 프로시저 PARTS_IN_ORDERS 특정 부품 번호를 포함 하는 주문의 목록을 포함 하는 결과 집합을 만든다고 가정 합니다. 다음 코드는 부품 번호 544에 대 한이 절차를 호출합니다.  
  
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
  
 응용 프로그램을 데이터 소스 프로시저를 지원 하는지 여부를 확인 하려면 호출 **SQLGetInfo** SQL_PROCEDURES 옵션을 사용 합니다.  
  
 프로시저에 대 한 자세한 내용은 참조 [프로시저](../../../odbc/reference/develop-app/procedures-odbc.md)합니다.
