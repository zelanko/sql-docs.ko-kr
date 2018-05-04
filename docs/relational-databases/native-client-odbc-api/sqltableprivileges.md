---
title: SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 19ee9ac71dc53124e3514a1fa57fc8f22a81e72f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLTablePrivileges** 는 정적 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 커서(키 집합 또는 동적 커서)에 대해 **SQLTablePrivileges** 를 실행하려고 하면 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO가 반환됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 사용 하 여 연결 된 서버의 테이블에 대 한 정보 보고를 지원는 *CatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLTablePrivileges 함수] (http://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API 구현 정보](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
