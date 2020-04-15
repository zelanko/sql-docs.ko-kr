---
title: SQLForeignKeys | 마이크로 소프트 문서
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b934ec05cf5f7b908efe83eeeb68bb358cd45156
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298493"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 외래 키 제약 조건 메커니즘을 통한 연속 업데이트 및 삭제를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 CASCADE 옵션이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_CASCADE를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 NO ACTION이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_NO_ACTION을 반환합니다.  
  
 **SQLForeignKeys** 매개 변수에 잘못된 값이 있으면 **SQLForeignKeys가** 실행 시 SQL_SUCCESS 반환합니다. **SQLFetch는** 이러한 매개 변수에 잘못된 값이 사용되는 SQL_NO_DATA 반환합니다.  
  
 **SQLForeignKeys정적** 서버 커서에서 실행할 수 있습니다. 업데이터(동적 또는 키 집합) 커서에서 **SQLForeignKeys를** 실행하려는 시도는 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
 네이티브 클라이언트 ODBC 드라이버는 *FKCatalogName 및 PKCatalogName* 매개 변수에 대한 두 부분으로 구성된 이름인 *Linked_Server_Name.Catalog_Name*수락하여 연결된 서버의 테이블에 대한 보고 정보를 지원합니다. *PKCatalogName* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [SQLForeignKeys 기능](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
