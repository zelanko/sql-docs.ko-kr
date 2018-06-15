---
title: 여러 결과 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be6cb4a2f7f03e63e3da9345b833b0382edd8e9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913848"
---
# <a name="multiple-results"></a>여러 결과
A *결과* 문제가 원본에서 반환 되는 데이터는 문이 실행 된 후입니다. ODBC에는 두 가지 유형의 결과: 결과 집합을 행 합니다. *행* 는 업데이트에 의해 영향을 받는 행의 수, 삭제 또는 insert 문이 됩니다. 에 설명 된 일괄 처리, [SQL 문 일괄 처리](../../../odbc/reference/develop-app/batches-of-sql-statements.md), 여러 개의 결과 생성할 수 있습니다.  
  
 다음 표에 **SQLGetInfo** 응용 프로그램 사용 하 여 데이터 원본 일괄 처리의 다른 유형 각각에 대해 여러 결과 반환 하는지 여부를 결정 하는 옵션입니다. 특히, 데이터 원본을 문의 전체 일괄 처리에 대 한 단일 행 수를 반환할 수 있습니다 또는 일괄 처리의 각 문에 대해 개별 행 개수입니다. 결과 집합 – 생성 문에 매개 변수 배열을 사용 하 여 실행의 경우 데이터 원본을 단일 결과 집합에 대 한 모든 매개 변수 집합을 반환할 수 또는 각 매개 변수 집합에 대 한 개별 결과 집합입니다.  
  
|일괄 처리 유형|행 개수|결과 집합|  
|----------------|----------------|-----------------|  
|명시적 일괄 처리|SQL_BATCH_ROW_COUNT [a]|-[b].|  
|절차|SQL_BATCH_ROW_COUNT [a]|-[b].|  
|매개 변수 배열|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 일괄 처리에서 문을 개수 – 생성은 지원 될 수, [a] 행 아직 행 개수 반환 되는 지원 되지 않습니다. SQL_BATCH_SUPPORT 옵션 **SQLGetInfo** 나타냅니다 행 개수 – 생성 문 일괄 처리에서 허용 여부 되지만 SQL_BATCH_ROW_COUNTS 옵션 행 개수 이러한 응용 프로그램에 반환 되는지 여부를 나타냅니다.  
  
 [b] 명시적 일괄 처리 및 프로시저 항상 반환 여러 개의 결과 집합이 여러 결과 집합 – 생성 문을 포함 합니다.  
  
> [!NOTE]  
>  여러 개의 결과 집합이 반환 될 수 있는지 여부에 대 한 일반적인 정보를 제공 하는 ODBC 1.0에 도입 된 SQL_MULT_RESULT_SETS 옵션입니다. 특히, SQL_BS_SELECT_EXPLICIT 또는 SQL_BS_SELECT_PROC 비트 SQL_BATCH_SUPPORT에 대해 반환 되는 경우 또는 SQL_PAS_BATCH SQL_PARAM_ARRAYS_SELECT에 대해 반환 되 면 "Y"로 설정 됩니다.  
  
 여러 개의 결과 처리 하려면 응용 프로그램이 호출 **SQLMoreResults**합니다. 이 함수는 현재 결과 삭제 하 고 결과 사용할 수 있도록 합니다. 결과가 더 이상 사용할 수 없는 경우 SQL_NO_DATA를 반환 합니다. 예를 들어 다음 문은 일괄 처리로 실행 됩니다.  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 응용 프로그램에서 만든 결과 집합에서 행을 인출 후 이러한 문을 실행 하는 **선택** 문. 가져오는 행을 완료 하는 경우 호출 **SQLMoreResults** 사용할 수 있도록 repriced 된 파트 수입니다. 필요한 경우 **SQLMoreResults** 반입 되지 않은 행을 삭제 하 고 커서를 닫습니다. 그런 다음 응용 프로그램 호출 **SQLRowCount** 부분에서 repriced 된 결정 하는 **업데이트** 문.  
  
 모든 결과 사용할 수 전에 전체 일괄 처리 문이 실행 되는 여부 드라이버 관련 됩니다. 이 경우; 일부 구현에서 호출, 다른 **SQLMoreResults** 일괄 처리의 다음 문으로 실행을 트리거합니다.  
  
 일괄 처리에서 문 중 하나가 실패 하면 **SQLMoreResults** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 문이 실패 했습니다 되거나 실패 한 문이 된 일괄 처리에서 마지막 문인 경우 일괄 처리가 중단 된 경우 **SQLMoreResults** SQL_ERROR를 반환 합니다. 문이 실패 하 고 실패 한 문을 일괄 처리의 마지막 문이 없습니다. 때 일괄 처리 중단 되지는 않은 경우 **SQLMoreResults** sql_success_with_info가 반환 됩니다. SQL_SUCCESS_WITH_INFO 하나 이상의 결과 집합 또는 개수를 생성 했음을 일괄 처리가 중단 되지 않았음을 나타냅니다.
