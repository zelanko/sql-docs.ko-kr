---
title: SQLForeignKeys | Microsoft Docs
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
helpviewer_keywords: SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e9c1f3fdbcf7767e2a9838130d620b6986f270d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 외래 키 제약 조건 메커니즘을 통한 연속 업데이트 및 삭제를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 CASCADE 옵션이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_CASCADE를 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 FOREIGN KEY 제약 조건의 ON UPDATE 및/또는 ON DELETE 절에 NO ACTION이 지정된 경우 UPDATE_RULE 및/또는 DELETE_RULE 열에 대해 SQL_NO_ACTION을 반환합니다.  
  
 잘못 된 값이 모든 있으면 **SQLForeignKeys** 매개 변수를 **SQLForeignKeys** 실행에 관계 없이 SQL_SUCCESS를 반환 합니다. **SQLFetch** 이러한 매개 변수에서 잘못 된 값을 사용할 경우 SQL_NO_DATA를 반환 합니다.  
  
 **SQLForeignKeys** 는 정적 서버 커서에 대해 실행할 수 있습니다. 실행 하려고 **SQLForeignKeys** 업데이트할 수 있는 (동적 또는 키 집합) 커서에서 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 두 부분으로 된 이름을 사용 하 여 연결 된 서버의 테이블에 대 한 정보 보고를 지원는 *FKCatalogName* 및 *PKCatalogName* 매개 변수:  *Linked_Server_Name.Catalog_Name*합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLForeignKeys 함수](http://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
