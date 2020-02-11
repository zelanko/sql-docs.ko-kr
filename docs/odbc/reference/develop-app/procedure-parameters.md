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
ms.openlocfilehash: f85512a1686df26cad739dc906e49cc5499f62e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912298"
---
# <a name="procedure-parameters"></a>프로시저 매개 변수
프로시저 호출의 매개 변수는 입력, 입/출력 또는 출력 매개 변수가 될 수 있습니다. 이는 항상 입력 매개 변수인 다른 모든 SQL 문의 매개 변수와는 다릅니다.  
  
 입력 매개 변수는 프로시저에 값을 보내는 데 사용 됩니다. 예를 들어 Parts 테이블에 PartID, 설명 및 가격 열이 있다고 가정 합니다. InsertPart 프로시저에는 테이블의 각 열에 대 한 입력 매개 변수가 있을 수 있습니다. 다음은 그 예입니다.  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 **Sqlexecdirect** 또는 **sqlexecute** 가 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_NO_DATA를 반환 하기 전 까지는 드라이버에서 입력 버퍼의 내용을 수정 하면 안 됩니다. **Sqlexecdirect** 또는 **sqlexecute** 가 SQL_NEED_DATA 또는 SQL_STILL_EXECUTING을 반환 하는 동안 입력 버퍼의 내용을 수정 하면 안 됩니다.  
  
 입력/출력 매개 변수는 프로시저에 값을 보내고 프로시저에서 값을 검색 하는 데 사용 됩니다. 입력 및 출력 매개 변수와 동일한 매개 변수를 사용 하는 것은 혼란 스 러 울 수 있으므로 피해 야 합니다. 예를 들어 프로시저가 주문 ID를 수락 하 고 고객의 ID를 반환 한다고 가정 합니다. 단일 입/출력 매개 변수를 사용 하 여 정의할 수 있습니다.  
  
```  
{call GetCustID(?)}  
```  
  
 주문 ID의 입력 매개 변수 및 고객 ID의 출력 또는 입/출력 매개 변수 등 두 개의 매개 변수를 사용 하는 것이 더 좋을 수 있습니다.  
  
```  
{call GetCustID(?, ?)}  
```  
  
 출력 매개 변수는 프로시저 반환 값을 검색 하 고 프로시저 인수에서 값을 검색 하는 데 사용 됩니다. 값을 반환 하는 프로시저를 *함수*라고도 합니다. 예를 들어 방금 언급 한 **GetCustID** 프로시저가 주문을 찾을 수 있는지 여부를 나타내는 값을 반환 한다고 가정 합니다. 다음 호출에서 첫 번째 매개 변수는 프로시저 반환 값을 검색 하는 데 사용 되는 출력 매개 변수이 고, 두 번째 매개 변수는 주문 ID를 지정 하는 데 사용 된 입력 매개 변수이 고, 세 번째 매개 변수는 고객 ID를 검색 하는 데 사용 되는 출력 매개 변수입니다.  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 드라이버는 다른 SQL 문에서 입력 매개 변수와 다른 방식으로 입력 및 입/출력 매개 변수의 값을 처리 합니다. 문이 실행 될 때 이러한 매개 변수에 바인딩된 변수 값을 검색 하 여 데이터 소스에 보냅니다.  
  
 문이 실행 된 후 드라이버는 입력/출력 및 출력 매개 변수의 반환 값을 해당 매개 변수에 바인딩된 변수에 저장 합니다. 이 반환 값은 프로시저에서 반환 된 모든 결과를 인출 하 고 **SQLMoreResults** 가 SQL_NO_DATA를 반환 하기 전 까지는 설정 되지 않을 수 있습니다. 문을 실행 하면 오류가 발생 하는 경우 입력/출력 매개 변수 버퍼 또는 출력 매개 변수 버퍼의 내용이 정의 되지 않습니다.  
  
 응용 프로그램은 **Sqlprocedure** 를 호출 하 여 프로시저에 반환 값이 있는지 여부를 확인 합니다. **SQLProcedureColumns** 를 호출 하 여 각 프로시저 매개 변수의 유형 (반환 값, 입력, 입/출력 또는 출력)을 확인 합니다.
