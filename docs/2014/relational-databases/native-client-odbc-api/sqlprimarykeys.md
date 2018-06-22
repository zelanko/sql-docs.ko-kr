---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cb0dc440025730c278206a751a5ce741b69b0f6e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081340"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  테이블에 하나 이상의 열에 고유 행 식별자로 사용 될 수 있는 하 고 PRIMARY KEY 제약 조건 없이 만들어진 SQLPrimaryKeys로 설정 하는 빈 결과 반환 합니다. ODBC 함수 [SQLSpecialColumns](sqlspecialcolumns.md) 보고서 행 식별자 후보 기본 키가 없는 테이블에 대 한 합니다.  
  
 SQLPrimaryKeys에 대 한 값이 존재 여부와 관계 없이 SQL_SUCCESS를 반환 *CatalogName*, *SchemaName*, 또는 *TableName* 매개 변수입니다. SQLFetch 이러한 매개 변수에서 잘못 된 값을 사용할 경우 SQL_NO_DATA를 반환 합니다.  
  
 SQLPrimaryKeys는 정적 서버 커서에 대해 실행할 수 있습니다. SQLPrimaryKeys 업데이트할 수 있는 (동적 또는 키 집합) 커서에 대해 실행 하려고 하면 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 사용 하 여 연결 된 서버의 테이블에 대 한 정보 보고를 지원는 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 및 테이블 반환 매개 변수  
 문 특성 SQL_SOPT_SS_NAME_SCOPE에 기본값인 SQL_SS_NAME_SCOPE_TABLE이 아니라 SQL_SS_NAME_SCOPE_TABLE_TYPE 값 있으면, SQLPrimaryKeys 테이블 형식의 기본 키 열에 대 한 정보를 반환 합니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 참조 하십시오. [SQLSetStmtAttr](sqlsetstmtattr.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLPrimaryKeys 함수](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  