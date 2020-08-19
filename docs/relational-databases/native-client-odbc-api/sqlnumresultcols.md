---
description: SQLNumResultCols
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2f4f868d9e32aa553930929cc0f713c9cc29136c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424035"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  실행된 문의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 결과 집합의 열 수를 보고할 때 서버에 연결하지 않습니다. 이 경우 **SQLNumResultCols** 를 호출하더라도 서버 왕복은 발생하지 않습니다. [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 및 [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)와 마찬가지로 준비되었지만 실행되지 않은 문에 대해 **SQLNumResultCols** 를 호출하면 서버 왕복이 발생합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문 일괄 처리에서 여러 결과 행 집합이 반환되는 경우 결과 집합 열의 수가 하나에서 다른 수로 변경될 수 있습니다. 이 경우 각 집합에 대해**SQLNumResultCols** 를 호출해야 합니다. 열 수가 변경되면 애플리케이션이 행 결과를 인출하기 전에 데이터 값을 다시 바인딩해야 합니다. 여러 결과 집합 반환을 처리하는 방법은 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 참조하십시오.  
  
 에서 시작 하는 데이터베이스 엔진의 향상 된 기능으로는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQLNumResultCols를 사용 하 여 예상 결과에 대 한 보다 정확한 설명을 얻을 수 있습니다. 이러한 보다 정확한 결과는 이전 버전의에서 SQLNumResultCols에서 반환 된 값과 다를 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLNumResultCols 함수](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
