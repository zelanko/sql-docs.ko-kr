---
title: 프로시저 매개 변수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cab0fea9c39e4946122698f2476668464e556c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861533"
---
# <a name="procedure-parameters"></a>프로시저 매개 변수
프로시저 호출에서 매개 변수 입력 될 수 있습니다, 입/출력 또는 출력 매개 변수입니다. 이 다른 모든 SQL 문의 경우 입력된 매개 변수는 항상의 매개 변수에서 다릅니다.  
  
 입력된 매개 변수 값을 보내는 절차로 사용 됩니다. 예를 들어 부품 테이블에 열이 PartID, 설명 및 가격입니다. InsertPart 프로시저 테이블의 각 열에 대 한 입력된 매개 변수가 있을 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 드라이버까지 입력된 버퍼의 내용을 수정 하지 않아야 **SQLExecDirect** 하거나 **SQLExecute** SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE, 또는 SQL_NO_DATA를 반환 합니다. 입력된 버퍼의 내용을 수정 하지 않아야 하는 동안 **SQLExecDirect** 하거나 **SQLExecute** SQL_NEED_DATA 또는 SQL_STILL_EXECUTING을 반환 합니다.  
  
 입/출력 매개 변수는 프로시저에 값을 보내고 프로시저에서 값을 검색에 모두 사용 됩니다. 동일한 매개 변수를 사용 하 여 입력 및 출력 매개 변수를 혼동 하는 경향이 및 피해 야 합니다. 예를 들어, 프로시저 주문 ID를 수락 하 고 고객의 ID를 반환 합니다. 이 단일 입/출력 매개 변수를 사용 하 여 정의할 수 있습니다.  
  
```  
{call GetCustID(?)}  
```  
  
 두 개의 매개 변수를 사용 하는 것이 더: 주문 ID와 출력 또는 고객 ID에 대 한 입/출력 매개 변수는 입력된 매개 변수:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 프로시저 반환 값을 검색 하 고 프로시저 인수;에서 값을 검색할 출력 매개 변수를 사용 합니다. 값을 반환 하는 프로시저 라고도 *함수*합니다. 예를 들어 합니다 **GetCustID** 프로시저가 방금 언급 한 순서를 찾을 수 있었는지 여부를 나타내는 값을 반환 합니다. 다음 호출에서 첫 번째 매개 변수는 프로시저 반환 값을 검색 하는 데 사용 하는 출력 매개 변수, 두 번째 매개 변수는 주문 ID를 지정 하는 데 사용 되는 입력된 매개 변수 및 세 번째 매개 변수는 고객 ID를 검색 하는 데 사용 하는 출력 매개 변수:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 드라이버 입력에 대 한 값을 처리 및 입/출력 프로시저의 매개 변수 이상 다른 SQL 문에 입력된 매개 변수를 다르게 합니다. 변수 값 검색 문이 실행 될 때 이러한 매개 변수에 바인딩되고 데이터 원본에 보낼 합니다.  
  
 문이 실행 된 후 드라이버 입/출력의 반환된 값 및 출력 매개 변수를 해당 매개 변수에 바인딩된 변수에 저장 합니다. 이러한 반환 값은 프로시저에서 반환 된 모든 결과 인출 된 후까지 설정할 보장 되지 하 고 **SQLMoreResults** SQL_NO_DATA를 반환 했습니다. 문을 실행 하면 오류가 발생을 입/출력 매개 변수 버퍼 또는 출력 매개 변수 버퍼의 내용을 정의 되지 않습니다.  
  
 응용 프로그램 호출 **SQLProcedure** 프로시저 반환 값을 갖는지 확인 합니다. 호출한 **SQLProcedureColumns** 각 프로시저 매개 변수의 (반환 값, 입력, 입/출력 또는 출력) 형식을 확인할 수 있습니다.
