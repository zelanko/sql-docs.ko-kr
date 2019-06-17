---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d59eb895b735771a94fa04745b492fc68eb2ea74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014515"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 외래 키 제약 조건 메커니즘을 통한 연속 업데이트 및 삭제를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 CASCADE 옵션이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_CASCADE를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 NO ACTION이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_NO_ACTION을 반환합니다.  
  
 잘못 된 값에 있는 경우 **SQLForeignKeys** 매개 변수 **SQLForeignKeys** 실행에 관계 없이 SQL_SUCCESS를 반환 합니다. **SQLFetch** 이러한 매개 변수에 잘못 된 값을 사용할 때에 SQL_NO_DATA를 반환 합니다.  
  
 **SQLForeignKeys** 는 정적 서버 커서에 대해 실행할 수 있습니다. 실행 하려고 **SQLForeignKeys** 업데이트 가능한 (동적 또는 키 집합) 커서에서 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 그대로 사용 하 여 연결 된 서버의 테이블에 대 한 보고 정보를 지원 합니다 *FKCatalogName* 하 고 *PKCatalogName* 매개 변수: *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>관련 항목  
 [SQLForeignKeys Function](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
