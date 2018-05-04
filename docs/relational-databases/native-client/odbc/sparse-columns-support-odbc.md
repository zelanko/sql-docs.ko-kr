---
title: 스파스 열 지원 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 46aa18d76f6acfc8e25054452dfe678f407e5b2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sparse-columns-support-odbc"></a>스파스 열 지원(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC의 스파스 열 지원에 대해 설명합니다. 스파스 열에 대 한 ODBC 지원을 보여 주는 샘플을 보려면 [스파스 열이 있는 테이블에 SQLColumns 호출](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)합니다. 스파스 열에 대한 자세한 내용은 [Sparse Columns Support in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)을 참조하십시오.  
  
## <a name="statement-metadata"></a>문 메타데이터  
 APD(응용 프로그램 매개 변수 설명자) 설명자 필드 및 SQL_SOPT_SS_NAME_SCOPE 문 특성에는 추가 값 SQL_SS_NAME_SCOPE_EXTENDED 및 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET을 사용할 수 있습니다. 이러한 값은 열에서 반환 된 결과 집합에 포함 된 지정 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)합니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 참조 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
 SQL_CA_SS_IS_COLUMN_SET이라는 읽기 전용 SQLSMALLINT 필드인 새 IRD(구현 행 설명자)를 사용하여 열이 XML **column_set** 값인지 여부를 확인할 수 있습니다. SQL_CA_SS_IS_COLUMN_SET에는 SQL_TRUE 및 SQL_FALSE 값을 사용할 수 있습니다.  
  
## <a name="catalog-metadata"></a>카탈로그 메타데이터  
 두 개의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 특정 열 (SS_IS_SPARSE 및 SS_IS_COLUMN_SET)의 결과 집합에 추가 된 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)합니다.  
  
## <a name="odbc-function-support-for-sparse-columns"></a>스파스 열에 대한 ODBC 함수 지원  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 다음과 같은 ODBC 함수가 스파스 열을 지원하도록 업데이트되었습니다.  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client & #40; ODBC & #41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
