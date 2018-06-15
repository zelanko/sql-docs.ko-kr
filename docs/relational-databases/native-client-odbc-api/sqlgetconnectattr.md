---
title: SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
caps.latest.revision: 60
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 36e0a367dfbdacb16dbd37ddbae68789f82b8781
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32948568"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 드라이버별 연결 특성을 정의합니다. 일부 특성은 **SQLGetConnectAttr**에서 사용할 수 있으며, 이 함수를 사용하여 현재 설정을 보고합니다. 이러한 특성 되지 않을 때까지 연결 된 또는 사용 하는 특성을 설정한 후에 대해 보고 하는 값 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)합니다.  
  
 이 항목에서는 읽기 전용 특성을 나열합니다. 다른 작업에 대 한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버별 연결 특성 참조 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)합니다.  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 SQL_COPT_SS_CONNECTION_DEAD 특성은 서버에 대한 연결 상태를 보고합니다. 드라이버는 현재 연결 상태에 대해 네트워크를 쿼리합니다.  
  
> [!NOTE]  
>  표준 ODBC 연결 특성 SQL_ATTR_CONNECTION_DEAD는 가장 최근 연결 상태를 반환합니다. 이 상태는 현재 연결 상태가 아닐 수도 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|SQL_CD_TRUE|서버에 대한 연결이 손실되었습니다.|  
|SQL_CD_FALSE|연결이 열려 있으며 문 처리에 사용할 수 있습니다.|  
  
## <a name="sqlcoptssclientconnectionid"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 SQL_COPT_SS_CLIENT_CONNECTION_ID 특성은 클라이언트 연결 ID를 검색하며, 이 ID를 사용하여 다음을 찾을 수 있습니다.  
  
-   설정할 경우 XEvents 로그의 진단 정보  
  
-   연결 링 버퍼의 연결 오류 정보  
  
-   설정할 경우 데이터 액세스 추적 로그의 진단 정보  
  
 자세한 내용은 참조 [확장 이벤트 로그의 진단 정보에 액세스](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|SQL_ERROR|연결하지 못했습니다.|  
|SQL_SUCCESS|연결이 성공했습니다. 출력 버퍼에서 클라이언트 연결 ID를 찾습니다.|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA 특성은 현재 드라이버 성능 통계가 포함된 SQLPERF 구조에 대한 포인터를 반환합니다. 성능 로깅이 사용되지 않는 경우**SQLGetConnectAttr** 에서 NULL을 반환합니다. SQLPERF 구조의 통계는 드라이버에서 동적으로 업데이트되지 않습니다. 성능 통계를 새로 고쳐야 할 때마다 **SQLGetConnectAttr** 을 호출합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|NULL|성능 로깅이 사용되지 않습니다.|  
|다른 모든 값|SQLPERF 구조에 대한 포인터입니다.|  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 장기 실행 쿼리 로깅이 사용되는 경우 SQL_COPT_SS_PERF_QUERY 특성에서 TRUE를 반환합니다. 쿼리 로깅이 활성화되지 않은 경우 요청에서 FALSE를 반환합니다.  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA 특성은 사용자 데이터 포인터를 검색합니다. 사용자 데이터는 클라이언트 소유의 메모리에 저장되고 연결별로 기록됩니다. 사용자 데이터 포인터가 설정되지 않은 경우 NULL 포인터인 SQL_UD_NOTSET가 반환됩니다.  
  
|Value|Description|  
|-----------|-----------------|  
|SQL_UD_NOTSET|사용자 데이터 포인터가 설정되어 있지 않습니다.|  
|다른 모든 값|사용자 데이터에 대한 포인터입니다.|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>SPN(서비스 사용자 이름)에 대한 SQLGetConnectAttr 지원  
 SQLGetConnectAttr 새 연결 특성인 SQL_COPT_SS_SERVER_SPN, SQL_COPT_SS_FAILOVER_PARTNER_SPN, SQL_COPT_SS_MUTUALLY_AUTHENTICATED 및 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD의 값을 쿼리할 데 사용할 수 있습니다. (SQLGetConnectOption 데도 사용할 수 있습니다 이러한 값을 쿼리할.)  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD는 Windows 인증을 사용하는 열린 연결에만 사용할 수 있습니다.  
  
 SQL_COPT_SS_SERVER_SPN 또는 SQL_COPT_SS_FAILOVER_PARTNER가 설정되지 않은 경우 기본값(빈 문자열)이 반환됩니다.  
  
 Spn에 대 한 자세한 내용은 참조 [서비스 사용자 이름 & #40; Spn & #41; 클라이언트 연결 & #40; ODBC & #41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="see-also"></a>관련 항목:  
 [SQLGetConnectAttr 함수](http://go.microsoft.com/fwlink/?LinkId=59347)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET quoted_identifier& #40; Transact SQL & #41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
