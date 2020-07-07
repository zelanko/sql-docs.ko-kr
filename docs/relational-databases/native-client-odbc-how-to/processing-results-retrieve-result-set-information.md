---
title: 결과 집합 정보 검색 (ODBC) | Microsoft Docs
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
ms.openlocfilehash: f00fe6310c339d7ec24736c5f659d3b7b7d84ce8
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006571"
---
# <a name="processing-results---retrieve-result-set-information"></a>결과 처리 - 결과 집합 정보 검색
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-get-information-about-a-result-set"></a>결과 집합에 대한 정보를 가져오려면  
  
1.  [Sqlnumresultcols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) 를 호출 하 여 결과 집합의 열 수를 가져옵니다.  
  
2.  결과 집합의 각 열에 대해 다음을 수행합니다.  
  
    -   [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 를 호출 하 여 결과 열에 대 한 정보를 가져옵니다.  
  
     또는  
  
    -   [Sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) 를 호출 하 여 결과 열에 대 한 특정 설명자 정보를 가져옵니다.  
  
## <a name="see-also"></a>참고 항목  
[ODBC&#41;&#40;결과 처리](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[ODBC&#41;&#40;결과 집합의 특징 확인](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
