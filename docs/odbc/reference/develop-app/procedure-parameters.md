---
title: 프로시저 매개변수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35d43ca7cf6e603d7dabca9eacf1e026daa753b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306962"
---
# <a name="procedure-parameters"></a>프로시저 매개 변수
프로시저 호출의 매개 변수는 입력, 입력/출력 또는 출력 매개 변수일 수 있습니다. 이는 항상 입력 매개 변수인 다른 모든 SQL 문의 매개 변수와 다릅니다.  
  
 입력 매개 변수는 프로시저에 값을 보내는 데 사용됩니다. 예를 들어 부품 테이블에 PartID, 설명 및 가격 열이 있다고 가정합니다. InsertPart 프로시저에는 테이블의 각 열에 대한 입력 매개 변수가 있을 수 있습니다. 다음은 그 예입니다.  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 **드라이버는 SQLExecDirect** 또는 **SQLExecute가** SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE 또는 SQL_NO_DATA 반환할 때까지 입력 버퍼의 내용을 수정해서는 안 됩니다. **SQLExecDirect** 또는 **SQLExecute가** SQL_NEED_DATA 또는 SQL_STILL_EXECUTING 반환하는 동안 입력 버퍼의 내용을 수정하면 안 됩니다.  
  
 입력/출력 매개 변수는 프로시저에 값을 보내고 프로시저에서 값을 검색하는 데 모두 사용됩니다. 입력 및 출력 매개 변수와 동일한 매개 변수를 사용하는 것은 혼동되는 경향이 있으며 피해야 합니다. 예를 들어 프로시저가 주문 ID를 수락하고 고객의 ID를 반환한다고 가정합니다. 단일 입력/출력 매개 변수로 정의할 수 있습니다.  
  
```  
{call GetCustID(?)}  
```  
  
 주문 ID에 대한 입력 매개 변수와 고객 ID에 대한 출력 또는 입력/출력 매개 변수의 두 가지 매개 변수를 사용하는 것이 좋습니다.  
  
```  
{call GetCustID(?, ?)}  
```  
  
 출력 매개 변수는 프로시저 반환 값을 검색하고 프로시저 인수에서 값을 검색하는 데 사용됩니다. 값을 반환하는 프로시저를 *함수라고도 합니다.* 예를 들어 방금 언급한 **GetCustID** 프로시저가 주문을 찾을 수 있는지 여부를 나타내는 값을 반환한다고 가정합니다. 다음 호출에서 첫 번째 매개 변수는 프로시저 반환 값을 검색하는 데 사용되는 출력 매개 변수이고, 두 번째 매개 변수는 order ID를 지정하는 데 사용되는 입력 매개 변수이고 세 번째 매개 변수는 고객 ID를 검색하는 데 사용되는 출력 매개 변수입니다.  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 드라이버는 프로시저의 입력 및 입력/출력 매개 변수에 대한 값을 다른 SQL 문의 입력 매개 변수와 다르지 않습니다. 문이 실행되면 이러한 매개 변수에 바인딩된 변수의 값을 검색하여 데이터 원본으로 보냅니다.  
  
 명령문이 실행된 후 드라이버는 해당 매개 변수에 바인딩된 변수에 입력/출력 및 출력 매개 변수의 반환된 값을 저장합니다. 이러한 반환된 값은 프로시저에서 반환된 모든 결과를 가져오고 **SQLMoreResults가** SQL_NO_DATA 반환될 때까지 설정되지 않습니다. 문을 실행하면 오류가 발생하면 입력/출력 매개 변수 버퍼 또는 출력 매개 변수 버퍼의 내용이 정의되지 않습니다.  
  
 응용 프로그램은 **SQLProcedure을** 호출하여 프로시저에 반환 값이 있는지 여부를 확인합니다. **SQLProcedureColumns를** 호출하여 각 프로시저 매개 변수의 형식(반환 값, 입력, 입력/출력 또는 출력)을 결정합니다.
