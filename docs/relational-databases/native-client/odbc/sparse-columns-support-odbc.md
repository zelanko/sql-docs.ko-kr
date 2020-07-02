---
title: 스파스 열 지원 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5724a0d0a083477c8f148fb80851ad8358dff2f1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787771"
---
# <a name="sparse-columns-support-odbc"></a>스파스 열 지원(ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC의 스파스 열 지원에 대해 설명합니다. 스파스 열에 대 한 ODBC 지원을 보여 주는 샘플은 [스파스 열이 있는 테이블에 대해 Sqlcolumns 호출](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)을 참조 하세요. 스파스 열에 대한 자세한 내용은 [Sparse Columns Support in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)을 참조하십시오.  
  
## <a name="statement-metadata"></a>문 메타데이터  
 APD(애플리케이션 매개 변수 설명자) 설명자 필드 및 SQL_SOPT_SS_NAME_SCOPE 문 특성에는 추가 값 SQL_SS_NAME_SCOPE_EXTENDED 및 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET을 사용할 수 있습니다. 이러한 값은 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)에서 반환하는 결과 집합에 포함할 열을 지정합니다. SQL_SOPT_SS_NAME_SCOPE에 대한 자세한 내용은 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 SQL_CA_SS_IS_COLUMN_SET이라는 읽기 전용 SQLSMALLINT 필드인 새 IRD(구현 행 설명자)를 사용하여 열이 XML **column_set** 값인지 여부를 확인할 수 있습니다. SQL_CA_SS_IS_COLUMN_SET에는 SQL_TRUE 및 SQL_FALSE 값을 사용할 수 있습니다.  
  
## <a name="catalog-metadata"></a>카탈로그 메타데이터  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [Sqlcolumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)의 결과 집합에 두 개의 특정 열 (SS_IS_SPARSE 및 SS_IS_COLUMN_SET)이 추가 되었습니다.  
  
## <a name="odbc-function-support-for-sparse-columns"></a>스파스 열에 대한 ODBC 함수 지원  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 다음과 같은 ODBC 함수가 스파스 열을 지원하도록 업데이트되었습니다.  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
