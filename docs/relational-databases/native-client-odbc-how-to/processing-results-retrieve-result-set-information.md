---
title: 결과 집합 정보 (ODBC) 검색 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b99d0b97179899b804a31b48a1334172e214f9f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133442"
---
# <a name="processing-results---retrieve-result-set-information"></a>결과 처리 - 결과 집합 정보 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-get-information-about-a-result-set"></a>결과 집합에 대한 정보를 가져오려면  
  
1.  호출 [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) 결과 집합의 열 개수를 가져올 수 있습니다.  
  
2.  결과 집합의 각 열에 대해 다음을 수행합니다.  
  
    -   호출 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 결과 열에 대 한 정보를 가져오려고 합니다.  
  
     또는  
  
    -   호출 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 결과 열에 대 한 특정 설명자 정보를 얻을 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[결과 처리 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[결과 집합의 특징을 확인 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
