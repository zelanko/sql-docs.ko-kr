---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 538b1a11962cf861aeaa1e95443f994b27feb87c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088663"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  테이블 열 또는 열에 고유 행 식별자로 사용할 수 있을 수 있습니다 하 고 PRIMARY KEY 제약 없이 만들어진 SQLPrimaryKeys로 설정 하는 빈 결과 반환 합니다. ODBC 함수 [SQLSpecialColumns](sqlspecialcolumns.md) 보고서 행 식별자 후보 기본 키가 없는 테이블입니다.  
  
 SQLPrimaryKeys 값 존재 여부와 관계 없이 SQL_SUCCESS를 반환 합니다 *CatalogName*하십시오 *SchemaName*, 또는 *TableName* 매개 변수입니다. 이러한 매개 변수에 잘못 된 값을 사용할 때 SQLFetch SQL_NO_DATA를 반환 합니다.  
  
 SQLPrimaryKeys는 정적 서버 커서에 대해 실행할 수 있습니다. SQLPrimaryKeys 업데이트 가능한 (동적 또는 키 집합) 커서에서 실행 하려고 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 그대로 사용 하 여 연결 된 서버의 테이블에 대 한 보고 정보를 지원 합니다 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 및 테이블 반환 매개 변수  
 문 특성 SQL_SOPT_SS_NAME_SCOPE에 기본값인 SQL_SS_NAME_SCOPE_TABLE이 아니라 SQL_SS_NAME_SCOPE_TABLE_TYPE 값 SQLPrimaryKeys 테이블 형식의 기본 키 열에 대 한 정보를 반환 합니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 참조 하세요. [SQLSetStmtAttr](sqlsetstmtattr.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLPrimaryKeys 함수](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
