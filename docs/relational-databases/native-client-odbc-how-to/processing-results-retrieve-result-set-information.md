---
title: 결과 집합 정보(ODBC) 검색 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f1c65841db0fdfd386891cfbd03bdee483ce25f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300393"
---
# <a name="processing-results---retrieve-result-set-information"></a>결과 처리 - 결과 집합 정보 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-get-information-about-a-result-set"></a>결과 집합에 대한 정보를 가져오려면  
  
1.  [SQLNumResultCols를](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) 호출하여 결과 집합의 열 수를 가져옵니다.  
  
2.  결과 집합의 각 열에 대해 다음을 수행합니다.  
  
    -   결과 열에 대 한 정보를 얻으려면 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 을 호출 합니다.  
  
     Or  
  
    -   [SQLColAttribute를](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 호출하여 결과 열에 대한 특정 설명자 정보를 가져옵니다.  
  
## <a name="see-also"></a>참고 항목  
[ODBC&#41;&#40;공정 결과](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[ODBC&#41;결과 집합의 특성 &#40;결정](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
