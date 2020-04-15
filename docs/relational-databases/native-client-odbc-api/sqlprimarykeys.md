---
title: SQL프라이어키 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2695d253030f13f71785046a25997ec6ee768622
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289037"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  테이블에는 고유 행 식별자로 사용할 수 있는 열이나 열이 있을 수 있으며, PRIMARY KEY 제약 조건 없이 만든 테이블에는 빈 결과 집합을 SQLPrimaryKeys로 반환합니다. ODBC 함수 [SQLSpecialColumns는](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md) 기본 키가 없는 테이블에 대한 행 식별자 후보를 보고합니다.  
  
 SQLPrimaryKeys는 *카탈로그 이름,* *스키마 이름*또는 *TableName* 매개 변수에 대한 값이 있는지 여부를 SQL_SUCCESS 반환합니다. 이 매개 변수에 잘못된 값이 사용되면 SQLFetch는 SQL_NO_DATA를 반환합니다.  
  
 SQLPrimary키는 정적 서버 커서에서 실행할 수 있습니다. 업데이터(동적 또는 키 집합) 커서에서 SQLPrimary키를 실행하려고 하면 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 *CatalogName* 매개 변수의 두 부분으로 구성된 이름인 *Linked_Server_Name.Catalog_Name*을 사용하여 연결된 서버의 테이블에 대한 정보를 보고할 수 있도록 지원합니다.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 및 테이블 반환 매개 변수  
 문 특성 SQL_SOPT_SS_NAME_SCOPE 기본값인 SQL_SS_NAME_SCOPE_TABLE 대신 SQL_SS_NAME_SCOPE_TABLE_TYPE 값이 있는 경우 SQLPrimaryKeys는 테이블 형식의 기본 키 열에 대한 정보를 반환합니다. SQL_SOPT_SS_NAME_SCOPE 대한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL주키 기능](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
