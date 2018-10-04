---
title: 서비스 사용자 이름 (Spn) 클라이언트 연결 (ODBC)에 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 1d60cb30-4c46-49b2-89ab-701e77a330a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f45e6124dbbad79802e290f935ccc6f3f45cee0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155353"
---
# <a name="service-principal-names-spns-in-client-connections-odbc"></a>클라이언트 연결(ODBC)의 SPN(서비스 사용자 이름)
  이 항목에서는 클라이언트 응용 프로그램의 SPN(서비스 사용자 이름)을 지원하는 ODBC 특성 및 함수에 대해 설명합니다. 클라이언트 응용 프로그램의 Spn에 대 한 자세한 내용은 참조 [서비스 사용자 이름 &#40;SPN&#41; 클라이언트 연결에 대 한 지원](../features/service-principal-name-spn-support-in-client-connections.md) 및 [상호 Kerberos 인증 가져오기](../../native-client-odbc-how-to/get-mutual-kerberos-authentication.md).  
  
## <a name="connection-string-keywords"></a>연결 문자열 키워드  
 클라이언트 응용 프로그램은 다음 연결 문자열 키워드를 사용하여 SPN을 지정할 수 있습니다.  
  
|키워드|값|  
|-------------|-----------|  
|`ServerSPN`|서버의 SPN입니다. 기본값은 빈 문자열이며 이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 드라이버에서 생성한 기본 SPN을 사용합니다.|  
|`FailoverPartnerSPN`|장애 조치(failover) 파트너의 SPN입니다. 기본값은 빈 문자열이며 이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 드라이버에서 생성한 기본 SPN을 사용합니다.|  
  
## <a name="connection-attributes"></a>연결 특성  
 클라이언트 응용 프로그램은 다음 연결 특성을 사용하여 SPN을 지정하고 인증 방법을 쿼리할 수 있습니다.  
  
|이름|형식|사용법|  
|----------|----------|-----------|  
|SQL_COPT_SS_SERVER_SPN<br /><br /> SQL_COPT_SS_FAILOVER_PARTNER_SPN|SQLTCHAR, 읽기/쓰기|서버의 SPN을 지정합니다. 기본값은 빈 문자열이며 이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 드라이버에서 생성한 기본 SPN을 사용합니다.<br /><br /> 이 특성은 프로그래밍 방식으로 설정된 후 또는 연결이 열린 후에만 쿼리할 수 있습니다. 열려 있지 않은 연결에서 이 특성을 쿼리하거나 특성이 프로그래밍 방식으로 설정되지 않은 경우 SQL_ERROR가 반환되고 SQLState 08003 및 "연결을 열 수 없습니다"라는 메시지가 표시되며 진단 레코드가 기록됩니다.<br /><br /> 연결이 열려 있을 때 이 특성을 설정하려고 하면 SQL_ERROR가 반환되고 SQLState HY011 및 "현재 작업이 잘못되었습니다"라는 메시지가 표시되며 진단 레코드가 기록됩니다.|  
|SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD|SQLTCHAR, 읽기 전용|연결에 사용된 인증 방법을 반환합니다. 응용 프로그램에 반환되는 값은 Windows에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에 반환하는 값입니다. 가능한 값은<br /><br /> -NTLM 인증을 사용 하 여 연결을 열 때 반환 되는 "NTLM"입니다.<br />-"Kerberos" Kerberos 인증을 사용 하 여 연결을 열 때 반환 됩니다.<br /><br /> 이 특성은 Windows 인증을 사용하여 열린 연결에 대해서만 읽을 수 있습니다. 연결이 열리기 전에 이 특성을 읽으려고 하면 SQL_ERROR가 반환되고 SQLState 08003 및 "연결을 열 수 없습니다"라는 메시지가 표시되며 오류가 기록됩니다.<br /><br /> Windows 인증을 사용하지 않은 연결에서 이 특성을 쿼리하면 SQL_ERROR가 반환되고 SQLState HY092 및 "잘못된 특성/옵션 식별자입니다(SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD는 트러스트된 연결에만 사용할 수 있음)"라는 메시지가 표시되며 오류가 기록됩니다.<br /><br /> 인증 방법을 확인할 수 없는 경우 SQL_ERROR가 반환되고 SQLState HY000 및 "일반 오류"라는 메시지가 표시되며 오류가 기록됩니다.|  
|SQL_COPT_SS_MUTUALLY_AUTHENTICATED|SQLSMALLINT, 읽기 전용|연결의 서버가 상호 인증되면 SQL_TRUE를 반환하고, 그렇지 않으면 SQL_FALSE를 반환합니다.<br /><br /> 이 특성은 열린 연결에 대해서만 읽을 수 있습니다. 연결이 열리기 전에 이 특성을 읽으려고 하면 SQL_ERROR가 반환되고 SQLState 08003 및 "연결을 열 수 없습니다"라는 메시지가 표시되며 오류가 기록됩니다.<br /><br /> Windows 인증을 사용하지 않은 연결에 대해 이 특성을 쿼리하면 SQL_FALSE가 반환됩니다.|  
  
## <a name="odbc-function-support-for-specifying-spns"></a>SPN 지정에 대한 ODBC 함수 지원  
 다음 ODBC 함수는 클라이언트 응용 프로그램 및 SPN을 지원합니다.  
  
-   [SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)  
  
-   [SQLConnect](../../native-client-odbc-api/sqlconnect.md)  
  
-   [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)  
  
-   [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md)  
  
-   [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
