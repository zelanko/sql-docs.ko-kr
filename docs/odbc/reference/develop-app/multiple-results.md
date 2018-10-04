---
title: 여러 결과 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7827a42a58e11847cdf9c3a63f4a7424eb5cfc5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654975"
---
# <a name="multiple-results"></a>여러 결과
A *결과* 항목이 반환 됩니다 데이터 원본에서 문을 실행 한 후입니다. ODBC에는 두 가지 유형의 결과: 결과 집합 및 행. *행* 업데이트에 의해 영향을 받는 행 수가 삭제 또는 삽입 됩니다. 일괄 처리에서 설명한 [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md), 여러 결과 생성할 수 있습니다.  
  
 다음 표에서 **SQLGetInfo** 응용 프로그램 사용 하 여 데이터 원본 일괄 처리의 다른 유형 각각에 대해 여러 결과 반환 하는지 여부를 결정 하는 옵션입니다. 특히 데이터 원본 문의 전체 일괄 처리에 대 한 단일 행 수를 반환 하거나 일괄 처리의 각 문에 대해 개별 행 개수입니다. 결과 집합 – 생성 문에 매개 변수 배열을 사용 하 여 실행의 경우 데이터 원본을 단일 결과 집합에 대 한 모든 매개 변수 집합을 반환할 수 있습니다 또는 개별 결과 집합이 각 매개 변수 집합에 대 한 합니다.  
  
|일괄 처리 유형|행 개수|결과 집합|  
|----------------|----------------|-----------------|  
|명시적 일괄 처리|[A] SQL_BATCH_ROW_COUNT|-[b|  
|프로시저|[A] SQL_BATCH_ROW_COUNT|-[b|  
|매개 변수 배열|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 행 개수 – 생성 문 일괄 처리에서 지원 될 수 있습니다, 아직 행 개수 반환 되는 지원 되지 않습니다. 옵션을 SQL_BATCH_SUPPORT **SQLGetInfo** 나타냅니다 행 개수 – 생성 문 일괄 처리에서 허용 됩니다 여부; SQL_BATCH_ROW_COUNTS 옵션은 응용 프로그램에 이러한 행 개수를 반환할지 여부를 나타냅니다.  
  
 [b] 명시적 일괄 처리 및 프로시저 여러 결과 집합 – 생성 문을 포함 하는 경우 여러 결과 집합을 반환할 항상.  
  
> [!NOTE]  
>  ODBC 1.0에 도입 된 SQL_MULT_RESULT_SETS 옵션은 여러 개의 결과 집합이 반환 될 수 있는지 여부에 대 한 일반적인 정보를 제공 합니다. 특히 SQL_BS_SELECT_EXPLICIT 또는 SQL_BS_SELECT_PROC 비트 SQL_BATCH_SUPPORT에 대해 반환 되는 경우 또는 SQL_PAS_BATCH SQL_PARAM_ARRAYS_SELECT에 대해 반환 되 면 "Y"로 설정 됩니다.  
  
 여러 결과 처리 하려면 응용 프로그램 호출 **SQLMoreResults**합니다. 이 함수는 현재 결과 삭제 하 고 결과 사용할 수 있도록 합니다. 더 이상 결과가 제공 될 경우 SQL_NO_DATA를 반환 합니다. 예를 들어 다음 문은 일괄 처리로 실행 됩니다.  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 응용 프로그램에서 만든 결과 집합에서 행을 인출 이러한 문을 실행 한 후 합니다 **선택** 문입니다. 행 페치 완료 되 면 호출 **SQLMoreResults** repriced 된 부분의 수 사용 가능 합니다. 필요한 경우 **SQLMoreResults** 인출된 된 행을 삭제 하 고 커서를 닫습니다. 그런 다음 응용 프로그램 호출 **SQLRowCount** 얼마나 많은 부분에서 repriced 것을 확인 하는 **업데이트** 문입니다.  
  
 모든 결과 사용할 수 전에 전체 일괄 처리 문을 실행 여부 드라이버별 인 합니다. 이 경우; 일부 구현 다른 호출 **SQLMoreResults** 일괄 처리의 다음 문으로 실행을 트리거합니다.  
  
 일괄 처리의 문 중 하나가 실패 하면 **SQLMoreResults** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 문이 실패 했습니다. 했거나 실패 한 문을 일괄 처리의 마지막 문이 때 일괄 처리 중단 되었으면 **SQLMoreResults** 에서 SQL_ERROR를 반환 합니다. 문이 실패 했습니다. 실패 한 문을 일괄 처리의 마지막 문이 없는 경우에 일괄 처리 중단 되지는 않은 경우 **SQLMoreResults** sql_success_with_info가 반환 됩니다. SQL_SUCCESS_WITH_INFO 하나 이상의 결과 집합 또는 count 생성 된 일괄 처리 중단 되지 않았음을 나타냅니다.
