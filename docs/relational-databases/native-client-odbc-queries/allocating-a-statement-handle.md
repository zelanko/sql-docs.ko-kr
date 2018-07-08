---
title: 문 핸들 할당 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fe5016a6f1adeaabfd5c0950634518ed3a26f578
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410962"
---
# <a name="allocating-a-statement-handle"></a>문 핸들 할당
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  응용 프로그램에서 문을 실행하려면 먼저 문 핸들을 할당해야 합니다. 호출 하는 것 **SQLAllocHandle** 사용 하 여는 *HandleType* 매개 변수 호출으로 설정 하 고 *InputHandle* 연결 핸들을 가리키는 합니다.  
  
 문 특성은 문 핸들의 특성입니다. 문 특성의 예로는 책갈피 사용 여부 및 문의 결과 집합에 사용할 커서의 종류를 들 수 있습니다. 사용 하 여 문 특성 설정 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)에 현재 설정을 사용 하 여 검색 됩니다 [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)합니다. 응용 프로그램에서 반드시 문 특성을 설정할 필요는 없습니다. 모든 문 특성에는 기본값이 있으며 일부 문 특성은 드라이버에 고유합니다.  
  
 몇 가지 ODBC 문 및 연결 옵션을 사용할 때는 주의를 기울여야 합니다. 호출 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 사용 하 여 *fOption* SQL_ATTR_LOGIN_TIMEOUT 컨트롤에 연결 (0을 설정 하기 위해 기다리는 동안 제한 시간에 대 한 연결 시도 대 한 응용 프로그램 대기 시간을 설정 이면 무기한 대기). 응답 시간이 느린 사이트의 경우 이 값을 높게 설정하여 연결을 완료하는 데 충분한 시간을 제공할 수 있습니다. 그러나 드라이버에서 연결할 수 없는 경우 사용자에게 적절한 시간 내에 응답되도록 간격을 항상 적절하게 설정해야 합니다.  
  
 호출 **SQLSetStmtAttr** 사용 하 여 *fOption* 장기 실행 쿼리에서 서버와 사용자를 보호 하기 위해 쿼리 시간 제한 간격을 설정 하는 SQL_ATTR_QUERY_TIMEOUT으로 설정 합니다.  
  
 호출 **SQLSetStmtAttr** 사용 하 여 *fOption* SQL_ATTR_MAX_LENGTH로 설정의 양을 제한 **텍스트** 고 **이미지** 데이터는는 개별 문이 검색할 수 있습니다. 호출 **SQLSetStmtAttr** 사용 하 여 *fOption* SQL_ATTR_MAX_ROWS로 설정 하기 위해 첫 번째 행 집합 제한 *n* 행 응용 프로그램 모든 경우에 필요 합니다. SQL_ATTR_MAX_ROWS를 설정하면 드라이버가 서버에 대해 SET ROWCOUNT 문을 실행합니다. 이 모든 변경 내용이 적용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문, 트리거 및 업데이트를 포함 합니다.  
  
 따라서 이러한 옵션을 설정할 때는 주의를 기울여야 합니다. 연결 핸들의 모든 문 핸들에 대한 SQL_ATTR_MAX_LENGTH 및 SQL_ATTR_MAX_ROWS 설정을 동일하게 지정하는 것이 좋습니다. 드라이버가 특정 문 핸들에서 이들 옵션 값이 다르게 설정된 다른 핸들로 전환하는 경우 설정을 변경하려면 드라이버가 적절한 SET TEXTSIZE 및 SET ROWCOUNT 문을 생성해야 합니다. 사용자 SQL 문은 일괄 처리의 첫 번째 문을 포함할 수 있으므로 드라이버는 이러한 문을 사용자 SQL 문과 동일한 일괄 처리에 배치할 수 없습니다. 드라이버는 SET TEXTSIZE 문과 SET ROWCOUNT 문을 별개의 일괄 처리로 보내야 하며 이 경우 추가 서버 왕복이 발생합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 실행 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
