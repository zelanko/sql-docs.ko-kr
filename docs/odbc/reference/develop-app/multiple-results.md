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
ms.openlocfilehash: f8679bea49b63ffd5dc7164942b42ac9eed7e9ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086361"
---
# <a name="multiple-results"></a>여러 결과
*결과* 는 문이 실행 된 후 데이터 원본에서 반환 되는 항목입니다. ODBC에는 결과 집합과 행 개수 라는 두 가지 유형의 결과가 있습니다. *행 개수* 는 update, delete 또는 insert 문의 영향을 받는 행의 수입니다. [SQL 문의 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md)로 설명 된 일괄 처리는 여러 결과를 생성할 수 있습니다.  
  
 다음 표에서는 응용 프로그램에서 각 유형의 일괄 처리에 대해 데이터 원본이 여러 결과를 반환 하는지 여부를 확인 하는 데 사용 하는 **SQLGetInfo** 옵션을 보여 줍니다. 특히 데이터 원본은 일괄 처리의 각 문에 대 한 전체 일괄 처리 또는 개별 행 개수에 대해 단일 행 개수를 반환할 수 있습니다. 매개 변수 배열을 사용 하 여 실행 되는 결과 집합 생성 문의 경우 데이터 원본은 각 매개 변수 집합에 대 한 모든 매개 변수 집합 또는 개별 결과 집합에 대해 단일 결과 집합을 반환할 수 있습니다.  
  
|일괄 처리 유형|행 개수|결과 집합|  
|----------------|----------------|-----------------|  
|명시적 일괄 처리|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|절차|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|매개 변수 배열|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 행 개수-일괄 처리에서 생성 문이 지원 될 수 있지만 행 수가 반환 될 수 없습니다. **SQLGetInfo** 의 SQL_BATCH_SUPPORT 옵션은 행 개수 생성 문이 일괄 처리에 허용 되는지 여부를 나타냅니다. SQL_BATCH_ROW_COUNTS 옵션은 이러한 행 개수가 응용 프로그램에 반환 되는지 여부를 나타냅니다.  
  
 [b] 명시적 일괄 처리 및 프로시저에는 여러 개의 결과 집합 생성 문이 포함 된 경우 항상 여러 결과 집합이 반환 됩니다.  
  
> [!NOTE]  
>  ODBC 1.0에 도입 된 SQL_MULT_RESULT_SETS 옵션은 여러 결과 집합을 반환할 수 있는지에 대 한 일반 정보만 제공 합니다. 특히 SQL_BATCH_SUPPORT에 대해 SQL_BS_SELECT_EXPLICIT 또는 SQL_BS_SELECT_PROC 비트가 반환 되거나 SQL_PARAM_ARRAYS_SELECT에 대해 SQL_PAS_BATCH 반환 되는 경우에는 "Y"로 설정 됩니다.  
  
 여러 결과를 처리 하기 위해 응용 프로그램은 **SQLMoreResults**를 호출 합니다. 이 함수는 현재 결과를 삭제 하 고 다음 결과를 사용할 수 있도록 합니다. 더 이상 결과를 사용할 수 없는 경우 SQL_NO_DATA를 반환 합니다. 예를 들어 다음 문이 일괄 처리로 실행 된다고 가정 합니다.  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 이러한 문이 실행 된 후 응용 프로그램은 **SELECT** 문에 의해 생성 된 결과 집합에서 행을 인출 합니다. 행을 인출 하는 작업이 완료 되 면 **SQLMoreResults** 를 호출 하 여 다시 가격이 책정 된 파트의 수를 사용할 수 있도록 합니다. 필요한 경우 **SQLMoreResults** 는 인출 되지 않은 행을 삭제 하 고 커서를 닫습니다. 그런 다음 응용 프로그램은 **Sqlrowcount** 를 호출 하 여 **UPDATE** 문에서 다시 가격이 책정 된 부분 수를 확인 합니다.  
  
 결과를 사용 하려면 전체 일괄 처리 문이 실행 되는지 여부에 관계 없이 드라이버에 한정 됩니다. 일부 구현에서는 이러한 경우가 발생 합니다. **SQLMoreResults** 를 호출 하면 일괄 처리에서 다음 문의 실행이 트리거됩니다.  
  
 일괄 처리의 문 중 하나가 실패 하면 **SQLMoreResults** 는 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO을 반환 합니다. 문이 실패 한 경우 일괄 처리가 중단 되었거나 실패 한 문이 일괄 처리의 마지막 문인 경우 **SQLMoreResults** 는 SQL_ERROR을 반환 합니다. 문이 실패 했을 때 일괄 처리가 중단 되지 않은 경우 실패 한 문이 일괄 처리의 마지막 문이 아니면 **SQLMoreResults** 는 SQL_SUCCESS_WITH_INFO을 반환 합니다. SQL_SUCCESS_WITH_INFO은 하나 이상의 결과 집합 또는 개수가 생성 되었으며 일괄 처리가 중단 되지 않았음을 나타냅니다.
