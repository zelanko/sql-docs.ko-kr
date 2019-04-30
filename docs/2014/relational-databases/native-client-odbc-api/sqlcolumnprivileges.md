---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 737ace72f201f3abe192393b1a1cc3747f5774e2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067759"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges** 값이 존재 하는지 여부에 관계 없이 SQL_SUCCESS를 반환 합니다*CatalogName*, *SchemaName*를 *TableName*, 또는  *ColumnName* 매개 변수입니다. **SQLFetch** 이러한 매개 변수에 잘못 된 값을 사용할 때에 SQL_NO_DATA를 반환 합니다.  
  
 **SQLColumnPrivileges** 는 정적 서버 커서에 대해 실행할 수 있습니다. 실행 하려고 **SQLColumnPrivileges** 업데이트 가능한 (동적 또는 키 집합) 커서에서 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 그대로 사용 하 여 연결 된 서버의 테이블에 대 한 보고 정보를 지원 합니다 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>관련 항목  
 [SQLColumnPrivileges 함수](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
