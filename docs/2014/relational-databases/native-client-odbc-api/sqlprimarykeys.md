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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf00ecd74b64b3910ba19365920baf914f86939c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705895"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  테이블에는 고유한 행 식별자로 사용할 수 있는 열이 있을 수 있으며, PRIMARY KEY 제약 조건 없이 만든 테이블은 SQLPrimaryKeys에 빈 결과 집합을 반환 합니다. ODBC 함수 [SQLSpecialColumns](sqlspecialcolumns.md) 는 기본 키가 없는 테이블에 대 한 행 식별자 후보를 보고 합니다.  
  
 SQLPrimaryKeys는 *CatalogName*, *SchemaName*또는 *TableName* 매개 변수에 대 한 값이 있는지 여부를 SQL_SUCCESS를 반환 합니다. 이 매개 변수에 잘못된 값이 사용되면 SQLFetch는 SQL_NO_DATA를 반환합니다.  
  
 SQLPrimaryKeys는 정적 서버 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 (동적 또는 키 집합) 커서에 대해 SQLPrimaryKeys를 실행 하려고 하면 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 *CatalogName* 매개 변수의 두 부분으로 구성된 이름인 *Linked_Server_Name.Catalog_Name*을 사용하여 연결된 서버의 테이블에 대한 정보를 보고할 수 있도록 지원합니다.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 및 테이블 반환 매개 변수  
 Statement 특성 SQL_SOPT_SS_NAME_SCOPE의 기본값 SQL_SS_NAME_SCOPE_TABLE이 아닌 SQL_SS_NAME_SCOPE_TABLE_TYPE 값이 있으면 SQLPrimaryKeys는 테이블 형식의 기본 키 열에 대 한 정보를 반환 합니다. SQL_SOPT_SS_NAME_SCOPE에 대 한 자세한 내용은 [SQLSetStmtAttr](sqlsetstmtattr.md)를 참조 하세요.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLPrimaryKeys 함수](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
