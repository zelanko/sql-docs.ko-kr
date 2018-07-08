---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d141beac8e581764ff5466dce343ad6335747a4e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407143"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  테이블 열 또는 열에 고유 행 식별자로 사용할 수 있을 수 있습니다 하 고 PRIMARY KEY 제약 없이 만들어진 SQLPrimaryKeys로 설정 하는 빈 결과 반환 합니다. ODBC 함수 [SQLSpecialColumns](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md) 보고서 행 식별자 후보 기본 키가 없는 테이블입니다.  
  
 SQLPrimaryKeys 값 존재 여부와 관계 없이 SQL_SUCCESS를 반환 합니다 *CatalogName*하십시오 *SchemaName*, 또는 *TableName* 매개 변수입니다. 이러한 매개 변수에 잘못 된 값을 사용할 때 SQLFetch SQL_NO_DATA를 반환 합니다.  
  
 SQLPrimaryKeys는 정적 서버 커서에 대해 실행할 수 있습니다. SQLPrimaryKeys 업데이트 가능한 (동적 또는 키 집합) 커서에서 실행 하려고 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 그대로 사용 하 여 연결 된 서버의 테이블에 대 한 보고 정보를 지원 합니다 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 및 테이블 반환 매개 변수  
 문 특성 SQL_SOPT_SS_NAME_SCOPE에 기본값인 SQL_SS_NAME_SCOPE_TABLE이 아니라 SQL_SS_NAME_SCOPE_TABLE_TYPE 값 SQLPrimaryKeys 테이블 형식의 기본 키 열에 대 한 정보를 반환 합니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 참조 하세요. [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLPrimaryKeys 함수](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
