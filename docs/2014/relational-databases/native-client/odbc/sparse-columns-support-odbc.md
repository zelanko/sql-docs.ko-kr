---
title: 스파스 열 지원 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e1583dad869860bdd2f555a354850c7f7a1198
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124333"
---
# <a name="sparse-columns-support-odbc"></a>스파스 열 지원(ODBC)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC의 스파스 열 지원에 대해 설명합니다. 스파스 열에 대 한 ODBC 지원을 보여 주는 샘플을 참조 하세요 [스파스 열이 있는 테이블에 SQLColumns 호출](../../native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)합니다. 스파스 열에 대한 자세한 내용은 [Sparse Columns Support in SQL Server Native Client](../features/sparse-columns-support-in-sql-server-native-client.md)을 참조하십시오.  
  
## <a name="statement-metadata"></a>문 메타데이터  
 APD(애플리케이션 매개 변수 설명자) 설명자 필드 및 SQL_SOPT_SS_NAME_SCOPE 문 특성에는 추가 값 SQL_SS_NAME_SCOPE_EXTENDED 및 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET을 사용할 수 있습니다. 이러한 값에서 반환 된 결과 집합에 포함 되는 열을 지정 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)합니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 참조 하세요. [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
 SQL_CA_SS_IS_COLUMN_SET이라는 읽기 전용 SQLSMALLINT 필드인 새 IRD(구현 행 설명자)를 사용하여 열이 XML `column_set` 값인지 여부를 확인할 수 있습니다. SQL_CA_SS_IS_COLUMN_SET에는 SQL_TRUE 및 SQL_FALSE 값을 사용할 수 있습니다.  
  
## <a name="catalog-metadata"></a>카탈로그 메타데이터  
 두 개의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 특정 열 (SS_IS_SPARSE 및 SS_IS_COLUMN_SET) 결과 집합에 추가 되었습니다 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)합니다.  
  
## <a name="odbc-function-support-for-sparse-columns"></a>스파스 열에 대한 ODBC 함수 지원  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서는 다음과 같은 ODBC 함수가 스파스 열을 지원하도록 업데이트되었습니다.  
  
-   [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
