---
title: 문 핸들 할당 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5c176536675af707ec2e16fde80028beba8a019a
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779986"
---
# <a name="allocating-a-statement-handle"></a>문 핸들 할당
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  애플리케이션에서 문을 실행하려면 먼저 문 핸들을 할당해야 합니다. *HandleType* 매개 변수가 SQL_HANDLE_STMT로 설정 되 고 연결 핸들을 가리키는 *InputHandle* **를 호출 하 여이** 를 수행 합니다.  
  
 문 특성은 문 핸들의 특성입니다. 문 특성의 예로는 책갈피 사용 여부 및 문의 결과 집합에 사용할 커서의 종류를 들 수 있습니다. [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 사용 하 여 문 특성을 설정 하 고 [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md)를 사용 하 여 현재 설정을 검색 합니다. 애플리케이션에서 반드시 문 특성을 설정할 필요는 없습니다. 모든 문 특성에는 기본값이 있으며 일부 문 특성은 드라이버에 고유합니다.  
  
 몇 가지 ODBC 문 및 연결 옵션을 사용할 때는 주의를 기울여야 합니다. *Foption* 을 SQL_ATTR_LOGIN_TIMEOUT로 설정 하 여 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 를 호출 하면 연결을 설정 하려고 대기 하는 동안 응용 프로그램에서 시간 초과가 발생 하기 전까지 대기 하는 시간을 제어 합니다 (0은 무한 대기를 지정 합니다). 응답 시간이 느린 사이트의 경우 이 값을 높게 설정하여 연결을 완료하는 데 충분한 시간을 제공할 수 있습니다. 그러나 드라이버에서 연결할 수 없는 경우 사용자에게 적절한 시간 내에 응답되도록 간격을 항상 적절하게 설정해야 합니다.  
  
 *Foption* 을 SQL_ATTR_QUERY_TIMEOUT로 설정 하 여 **SQLSetStmtAttr** 를 호출 하면 서버 및 사용자가 장기 실행 쿼리를 보호 하는 데 도움이 되는 쿼리 시간 제한 간격이 설정 됩니다.  
  
 *Foption* 을 SQL_ATTR_MAX_LENGTH로 설정 하 여 **SQLSetStmtAttr** 를 호출 하면 개별 문이 검색할 수 있는 **텍스트** 및 **이미지** 데이터의 양이 제한 됩니다. *Foption* 을 SQL_ATTR_MAX_ROWS로 설정 하 여 **SQLSetStmtAttr** 를 호출 하면 모든 응용 프로그램에 필요한 경우 행 집합을 처음 *n 개* 행으로 제한 합니다. SQL_ATTR_MAX_ROWS를 설정하면 드라이버가 서버에 대해 SET ROWCOUNT 문을 실행합니다. 이는 트리거와 업데이트를 포함 하 여 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문에 영향을 줍니다.  
  
 따라서 이러한 옵션을 설정할 때는 주의를 기울여야 합니다. 연결 핸들의 모든 문 핸들에 대한 SQL_ATTR_MAX_LENGTH 및 SQL_ATTR_MAX_ROWS 설정을 동일하게 지정하는 것이 좋습니다. 드라이버가 특정 문 핸들에서 이들 옵션 값이 다르게 설정된 다른 핸들로 전환하는 경우 설정을 변경하려면 드라이버가 적절한 SET TEXTSIZE 및 SET ROWCOUNT 문을 생성해야 합니다. 사용자 SQL 문은 일괄 처리의 첫 번째 문을 포함할 수 있으므로 드라이버는 이러한 문을 사용자 SQL 문과 동일한 일괄 처리에 배치할 수 없습니다. 드라이버는 SET TEXTSIZE 문과 SET ROWCOUNT 문을 별개의 일괄 처리로 보내야 하며 이 경우 추가 서버 왕복이 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 쿼리 &#40;실행&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
