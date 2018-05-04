---
title: SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41754d26ccaf240018db0060a51c33622b06ddaf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  문 실행을 위해 매개 변수 값의 배열을 바인딩한 경우 문 실행 시 매개 변수 값의 행 중 하나라도 오류 조건을 생성하면 **SQLRowCount** 는 SQL_ERROR를 반환합니다. 이 함수의 *RowCountPtr* 인수를 통해서는 값이 반환되지 않습니다.  
  
 응용 프로그램에서는 SQL_ATTR_PARAMS_PROCESSED_PTR 매개 변수 특성을 사용하여 오류가 발생하기 전에 처리된 매개 변수 수를 캡처할 수 있습니다.  
  
 또한 응용 프로그램에서는 SQL_ATTR_PARAM_STATUS_PTR 문 특성을 사용하여 바인딩된 상태 값의 배열을 사용하여 문제를 일으키는 매개 변수 행의 배열 오프셋을 캡처할 수도 있습니다. 응용 프로그램에서는 상태 배열을 트래버스하여 처리된 실제 행 수를 확인할 수 있습니다.  
  
 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT, UPDATE, DELETE 또는 MERGE 문의 OUTPUT 절이 실행 되 고, SQLRowCount OUTPUT 절에 의해 생성 된 결과 집합의 모든 행이 소비 될 때까지 영향을 받는 행의 수를 반환 하지 것입니다. 소비 하려면 이러한 행 또는 호출할 있습니다 SQLFetch SQLFetchScroll입니다. 모든 결과 행이 소비 될 때까지 SQLResultCols-1을 반환 합니다. SQLFetch 또는 SQLFetchScroll sql_no_data가 반환 된 후 응용 프로그램 하 여 다음 결과로 이동 하려면 SQLMoreResults를 호출 하기 전에 영향을 받는 행 수를 확인 하려면 SQLRowCount 호출 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLRowCount 함수](http://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
