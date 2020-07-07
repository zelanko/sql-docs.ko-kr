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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f50bb8fef06d42432fc0a223805b4a1f2d161aa0
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003523"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 외래 키 제약 조건 메커니즘을 통한 연속 업데이트 및 삭제를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 CASCADE 옵션이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_CASCADE를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 NO ACTION이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_NO_ACTION을 반환합니다.  
  
 **SQLForeignKeys** 매개 변수에 잘못 된 값이 있는 경우 **SQLForeignKeys** 은 실행 시 SQL_SUCCESS 반환 합니다. 이러한 매개 변수에 잘못 된 값이 사용 되는 경우 **Sqlfetch** SQL_NO_DATA 반환 합니다.  
  
 **SQLForeignKeys** 는 정적 서버 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 (동적 또는 키 집합) 커서에 대해 **SQLForeignKeys** 를 실행 하려고 하면 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 *FKCatalogName* 및 *PKCatalogName* 매개 변수에 대해 두 부분으로 구성 된 이름 ( *Linked_Server_Name. Catalog_Name*를 수락 하 여 연결 된 서버의 테이블에 대 한 보고 정보를 지원 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLForeignKeys 함수](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
