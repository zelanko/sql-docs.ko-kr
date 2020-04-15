---
title: 여러 결과 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d90414b631a7e81a7868ab7974b64ea84a0ea452
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302417"
---
# <a name="multiple-results"></a>여러 결과
*결과는* 문이 실행된 후 데이터 원본에서 반환되는 것입니다. ODBC에는 결과 집합과 행 개수의 두 가지 유형의 결과가 있습니다. *행 수는* 업데이트, 삭제 또는 삽입 문의 영향을 받는 행 수입니다. [SQL 문 일괄 처리에](../../../odbc/reference/develop-app/batches-of-sql-statements.md)설명된 일괄 처리는 여러 결과를 생성할 수 있습니다.  
  
 다음 표에는 데이터 원본이 각 다른 배치 유형에 대해 여러 결과를 반환하는지 여부를 결정하기 위해 응용 프로그램에서 사용하는 **SQLGetInfo** 옵션이 나열되어 있습니다. 특히 데이터 원본은 일괄 처리의 각 문에 대한 전체 명령문 또는 개별 행 개수에 대한 단일 행 수를 반환할 수 있습니다. 매개 변수 배열로 실행되는 결과 집합 생성 문의 경우 데이터 원본은 각 매개 변수 집합에 대한 모든 매개 변수 집합 또는 개별 결과 집합에 대한 단일 결과 집합을 반환할 수 있습니다.  
  
|배치 유형|행 수|결과 집합|  
|----------------|----------------|-----------------|  
|명시적 일괄 처리|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|절차|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|매개 변수 배열|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 일괄 처리의 행 개수 생성 문이 지원될 수 있지만 행 카운트의 반환은 지원되지 않습니다. **SQLGetInfo의** SQL_BATCH_SUPPORT 옵션은 행 개수 생성 문이 일괄 처리에서 허용되는지 여부를 나타냅니다. SQL_BATCH_ROW_COUNTS 옵션은 이러한 행 수가 응용 프로그램에 반환되는지 여부를 나타냅니다.  
  
 [b] 명시적 일괄 처리 및 프로시저는 항상 여러 결과 집합 생성 문을 포함하는 경우 여러 결과 집합을 반환합니다.  
  
> [!NOTE]  
>  ODBC 1.0에 도입된 SQL_MULT_RESULT_SETS 옵션은 여러 결과 집합을 반환할 수 있는지 여부에 대한 일반적인 정보만 제공합니다. 특히 SQL_BS_SELECT_EXPLICIT 또는 SQL_BS_SELECT_PROC 비트가 SQL_BATCH_SUPPORT 반환되거나 SQL_PARAM_ARRAYS_SELECT SQL_PAS_BATCH 반환되는 경우 "Y"로 설정됩니다.  
  
 여러 결과를 처리하기 위해 응용 프로그램은 **SQLMoreResults**를 호출합니다. 이 함수는 현재 결과를 삭제하고 다음 결과를 사용할 수 있게 합니다. 더 이상 결과를 사용할 수 없는 경우 SQL_NO_DATA 반환합니다. 예를 들어 다음 문이 일괄 처리로 실행된다고 가정합니다.  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 이러한 문이 실행된 후 응용 프로그램은 **SELECT** 문에 의해 생성된 결과 집합에서 행을 가져옵니다. 행을 가져오면 **SQLMoreResults를** 호출하여 가격이 책정된 부품 수를 사용할 수 있도록 합니다. 필요한 경우 **SQLMoreResults는** 페치되지 않은 행을 삭제하고 커서를 닫습니다. 그런 다음 응용 프로그램은 **SQLRowCount를** 호출하여 **UPDATE** 문에 의해 재평가된 부품 수를 확인합니다.  
  
 결과를 사용할 수 있기 전에 전체 일괄 처리 문이 실행되는지 여부는 드라이버에 따라 다릅니다. 일부 구현에서는 이러한 경우가 있습니다. 다른 경우 **SQLMoreResults호출하면** 일괄 처리에서 다음 명령문의 실행이 트리거됩니다.  
  
 일괄 처리의 명령문 중 하나가 실패하면 **SQLMoreResults는** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환합니다. 명령문이 실패하거나 실패한 문이 일괄 처리의 마지막 문일 때 일괄 처리가 중단된 경우 **SQLMoreResults는** SQL_ERROR 반환합니다. 명령문이 실패하고 실패한 문이 일괄 처리의 마지막 문이 아닐 때 일괄 처리가 중단되지 않은 경우 **SQLMoreResults는** SQL_SUCCESS_WITH_INFO 반환합니다. SQL_SUCCESS_WITH_INFO 하나 이상의 결과 집합 또는 개수가 생성되었으며 일괄 처리가 중단되지 않음을 나타냅니다.
