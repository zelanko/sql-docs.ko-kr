---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 862796aba363d2d7811a7e2d557dbf38a9280085
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumnPrivileges** 에 대 한 값이 존재 하는지 여부에 관계 없이 SQL_SUCCESS를 반환 된*CatalogName*, *SchemaName*, *TableName*, 또는  *ColumnName* 매개 변수입니다. **SQLFetch** 이러한 매개 변수에서 잘못 된 값을 사용할 경우 SQL_NO_DATA를 반환 합니다.  
  
 **SQLColumnPrivileges** 는 정적 서버 커서에 대해 실행할 수 있습니다. 실행 하려고 **SQLColumnPrivileges** 업데이트할 수 있는 (동적 또는 키 집합) 커서에서 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 사용 하 여 연결 된 서버의 테이블에 대 한 정보 보고를 지원는 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLColumnPrivileges 함수](http://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
