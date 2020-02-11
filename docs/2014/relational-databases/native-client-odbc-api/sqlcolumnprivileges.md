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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067759"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **Sqlcolumnprivileges** *CatalogName*, *SchemaName*, *TableName*또는 *ColumnName* 매개 변수에 대 한 값이 있는지 여부를 SQL_SUCCESS를 반환 합니다. 이러한 매개 변수에 잘못 된 값이 사용 되는 경우 **Sqlfetch** SQL_NO_DATA 반환 합니다.  
  
 **Sqlcolumnprivileges** 정적 서버 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 (동적 또는 키 집합) 커서에 대해 **Sqlcolumnprivileges** 실행 시도는 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환 됩니다.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 *CatalogName* 매개 변수의 두 부분으로 구성된 이름인 *Linked_Server_Name.Catalog_Name*을 사용하여 연결된 서버의 테이블에 대한 정보를 보고할 수 있도록 지원합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLColumnPrivileges 함수](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
