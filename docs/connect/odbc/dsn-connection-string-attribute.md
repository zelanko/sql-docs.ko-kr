---
title: DSN 및 연결 문자열 키워드 및 SQL Server 용 ODBC 드라이버에서 사용 되는 특성 | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
- DSN
- Connection String Keywords
- Connection Attributes
ms.tgt_pltfrm: ''
ms.topic: article
author: MightyPen
ms.author: v-jizho2
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 641d0cf4134dc488436f981df1d4bee2c089acd2
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="dsn-and-connection-string-keywords-and-attributes"></a>DSN 및 연결 문자열 키워드 및 특성

이 페이지 SQLSetConnectAttr 및 ODBC Driver for SQL Server에서에서 사용할 수 있는 SQLGetConnectAttr에 대 한 연결 문자열 및 Dsn에 대 한 키워드 및 연결 특성을 나열합니다.



## <a name="supported-dsnconnection-string-keywords-and-connection-attributes"></a>지원 되는 DSN/연결 문자열 키워드 및 연결 특성

다음 표에 사용 가능한 키워드 및 각 플랫폼 (l: Linux;에 대 한 특성 M: Mac; W: Windows)
키워드 또는 특성에 대 한 자세한 내용을 보려면 클릭 합니다.

| DSN / 연결 문자열 키워드 | 연결 특성입니다. | 플랫폼 | 
|-|-|-|
| [Addr](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [주소](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [AnsiNPW](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) |  [SQL_COPT_SS_ANSI_NPW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssansinpw) | LMW |
| [APP](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ApplicationIntent](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_APPLICATION_INTENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssapplicationintent) | LMW |
| [AttachDBFileName](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ATTACHDBFILENAME](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssattachdbfilename) | LMW |
| [인증](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sqlcoptssauthentication) | [SQL_COPT_SS_AUTHENTICATION](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sqlcoptssauthentication) | LMW |
| [AutoTranslate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRANSLATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstranslate) | LMW |
| [ColumnEncryption](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sqlcoptsscolumnencryption) | [SQL_COPT_SS_COLUMN_ENCRYPTION](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sqlcoptsscolumnencryption) | LMW |
| [ConnectRetryCount](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_COUNT](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [ConnectRetryInterval](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_INTERVAL](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [데이터베이스](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_ATTR_CURRENT_CATALOG](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| [설명](../../connect/odbc/dsn-connection-string-attribute.md#description) | | LMW |
| [드라이버](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [DSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Encrypt](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ENCRYPT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssencrypt) | LMW |
| [Failover_Partner](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssfailoverpartner) | W |
| [FailoverPartnerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | W |
| [FileDSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [KeystoreAuthentication](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystorePrincipalId](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystoreSecret](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [언어](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [MARS_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MARS_ENABLED](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmarsenabled) | LMW |
| [MultiSubnetFailover](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MULTISUBNET_FAILOVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmultisubnetfailover) | LMW |
| [Net](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [네트워크](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [PWD](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [QueryLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquery) | W |
| [QueryLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquerylog) | W |
| [QueryLogTIme](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_INTERVAL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfqueryinterval) | W |
| [QuotedId](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_QUOTED_IDENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssquotedident) | LMW |
| [지역](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [SaveFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Server](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ServerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_SERVER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| [StatsLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdata) | W |
| [StatsLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalog) | W |
| [TransparentNetworkIPResolution](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sqlcoptsstnir) | [SQL_COPT_SS_TNIR](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sqlcoptsstnir) | LMW |
| [Trusted_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_INTEGRATED_SECURITY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssintegratedsecurity) | LMW |
| [TrustServerCertificate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRUST_SERVER_CERTIFICATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstrustservercertificate) | LMW |
| [UID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [UseFMTONLY](../../connect/odbc/dsn-connection-string-attribute.md#usefmtonly) | | LMW |
| [WSID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| | [SQL_ATTR_ACCESS_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ACCESS_MODE) | LMW |
| | [SQL_ATTR_ASYNC_DBC_EVENT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCALLBACK](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCONTEXT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_AUTO_IPD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_AUTOCOMMIT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_AUTOCOMMIT) | LMW |
| | [SQL_ATTR_CONNECTION_DEAD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_CONNECTION_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_DBC_INFO_TOKEN](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_LOGIN_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_LOGIN_TIMEOUT) | LMW |
| | [SQL_ATTR_METADATA_ID](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_ODBC_CURSORS](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ODBC_CURSORS) | LMW |
| | [SQL_ATTR_PACKET_SIZE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_PACKET_SIZE) | LMW |
| | [SQL_ATTR_QUIET_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_QUIET_MODE) | LMW |
| | [SQL_ATTR_RESET_CONNECTION](../../odbc/reference/develop-driver/upgrading-a-3-5-driver-to-a-3-8-driver.md#connection-pooling) <br> (SQL_COPT_SS_RESET_CONNECTION) | LMW |  
| | [SQL_ATTR_TRACE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACE) | LMW |
| | [SQL_ATTR_TRACEFILE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACEFILE) | LMW |
| | [SQL_ATTR_TRANSLATE_LIB](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_DLL) | LMW |
| | [SQL_ATTR_TRANSLATE_OPTION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_OPTION) | LMW |
| | [SQL_ATTR_TXN_ISOLATION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TXN_ISOLATION) | LMW |
| | [SQL_COPT_SS_ACCESS_TOKEN](dsn-connection-string-attribute.md#sqlcoptssaccesstoken) | LMW |
| | [SQL_COPT_SS_ANSI_OEM](dsn-connection-string-attribute.md#sqlcoptssansioem)| W |
| | [SQL_COPT_SS_BCP](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbcp) | LMW |
| | [SQL_COPT_SS_BROWSE_CACHE_DATA](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) | LMW |
| | [SQL_COPT_SS_BROWSE_CONNECT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseconnect) | LMW |
| | [SQL_COPT_SS_BROWSE_SERVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseserver) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREDATA](dsn-connection-string-attribute.md#sqlcoptsscekeystoredata) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREPROVIDER](dsn-connection-string-attribute.md#sqlcoptsscekeystoreprovider) | LMW |
| | [SQL_COPT_SS_CLIENT_CONNECTION_ID](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md#sqlcoptssclientconnectionid) | LMW |
| | [SQL_COPT_SS_CONCAT_NULL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconcatnull) | LMW |
| | [SQL_COPT_SS_CONNECTION_DEAD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconnectiondead) | LMW |
| | [SQL_COPT_SS_ENLIST_IN_DTC](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistindtc) | W |
| | [SQL_COPT_SS_ENLIST_IN_XA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistinxa) | W |
| | [SQL_COPT_SS_FALLBACK_CONNECT](dsn-connection-string-attribute.md#sqlcoptssfallbackconnect) | LMW |
| | [SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_MUTUALLY_AUTHENTICATED](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_OLDPWD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssoldpwd) | LMW |
| | [SQL_COPT_SS_PERF_DATA_LOG_NOW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalognow) | W |
| | [SQL_COPT_SS_PRESERVE_CURSORS](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsspreservecursors) | LMW |
| | [SQL_COPT_SS_TXN_ISOLATION](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstxnisolation) | LMW |
| | [SQL_COPT_SS_USER_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssuserdata) | LMW |
| | [SQL_COPT_SS_WARN_ON_CP_ERROR](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsswarnoncperror) | LMW |


다음은 몇 가지 연결 문자열 키워드 및 연결 특성에 문서화 되지 않은 [Connection String Keywords with SQL Server Native Client를 사용 하 여](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md), [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLSetConnectAttr 함수](../../odbc/reference/syntax/sqlsetconnectattr-function.md)합니다.

### <a name="description"></a>Description

데이터 원본을 설명 하는 데 사용 합니다.

### <a name="sqlcoptssansioem"></a>SQL_COPT_SS_ANSI_OEM

ANSI에서 OEM으로의 변환 데이터 제어 합니다. 

| 특성 값 | Description |
|-|-|
| SQL_AO_OFF | (기본값) 변환이 수행 되지 않습니다. |
| SQL_AO_ON | 변환이 수행 됩니다. |

### <a name="sqlcoptssfallbackconnect"></a>SQL_COPT_SS_FALLBACK_CONNECT

SQL Server 대체 (fallback) 연결의 사용을 제어 합니다. 이 더 이상 지원 됩니다.

| 특성 값 | Description |
|-|-|
| SQL_FB_OFF | (기본값) 대체 (fallback) 연결을 사용할 수 있습니다. |
| SQL_FB_ON | 대체 (fallback) 연결이 설정 되어 있습니다. |



## <a name="new-connection-string-keywords-and-connection-attributes"></a>새 연결 문자열 키워드 및 연결 특성

###  <a name="authentication---sqlcoptssauthentication"></a>인증-SQL_COPT_SS_AUTHENTICATION

SQL Server에 연결할 때 사용할 인증 모드를 설정 합니다. 참조 [Azure Active Directory를 사용 하 여](using-azure-active-directory.md) 자세한 정보에 대 한 합니다.

| 키워드 값 | 특성 값 | Description |
|-|-|-|
| |SQL_AU_NONE|(기본값) 설정 되지 않았습니다. 인증 모드를 결정 하는 다른 특성의 조합 합니다.|
|SqlPassword|SQL_AU_PASSWORD|SQL Server 인증 사용자 이름 및 암호입니다.|
|ActiveDirectoryIntegrated|SQL_AU_AD_INTEGRATED|Azure Active Directory 통합 인증입니다.|
|ActiveDirectoryPassword|SQL_AU_AD_PASSWORD|Azure Active Directory 암호 인증입니다.|
|ActiveDirectoryInteractive|SQL_AU_AD_INTERACTIVE|Azure Active Directory 대화형 인증입니다.|
| |SQL_AU_RESET|설정 되지 않은 경우. 모든 DSN 또는 연결 문자열 설정을 재정의합니다.|

### <a name="columnencryption---sqlcoptsscolumnencryption"></a>ColumnEncryption - SQL_COPT_SS_COLUMN_ENCRYPTION

투명 한 열 암호화 (상시 암호화)를 제어합니다. 참조 [항상 암호화를 사용 하 여 (ODBC)](using-always-encrypted-with-the-odbc-driver.md) 자세한 정보에 대 한 합니다.

| 키워드 값 | 특성 값 | Description |
|-|-|-|
|설정|SQL_CE_ENABLED|상시 암호화를 사용 합니다.|
|사용 안 함|SQL_CE_DISABLED|(기본값) 상시 암호화를 해제 합니다.|
| |SQL_CE_RESULTSETONLY|암호 해독만 (결과 및 반환 값)을 사용 하도록 설정 합니다.|

### <a name="transparentnetworkipresolution---sqlcoptsstnir"></a>TransparentNetworkIPResolution - SQL_COPT_SS_TNIR

컨트롤 더 빠르게 다시 연결할 수 있도록 MultiSubnetFailover와 상호 작용 하는 투명 네트워크 IP 확인 기능을 시도 합니다. 참조 [투명 네트워크 IP 확인 사용 하 여](using-transparent-network-ip-resolution.md) 자세한 정보에 대 한 합니다.

| 키워드 값 | 특성 값| Description |
|-|-|-|
|예|SQL_IS_ON|(기본값) 투명 네트워크 IP 확인을 수 있습니다.|
|아니요|SQL_IS_OFF|투명 네트워크 IP 확인을 사용 하지 않도록 설정 합니다.|

### <a name="usefmtonly"></a>UseFMTONLY

SQL Server 2012에 연결 하 고 새 메타 데이터에 대 한 SET FMTONLY의 사용을 제어 합니다.

| 키워드 값 | Description |
|-|-|
|아니요|(기본값) 사용 가능한 경우 메타 데이터에 대 한 sp_describe_first_result_set을 사용 합니다. |
|예| 메타 데이터에 대 한 SET FMTONLY를 사용 합니다. |

### <a name="sqlcoptssaccesstoken"></a>SQL_COPT_SS_ACCESS_TOKEN

인증을 위해 Azure Active Directory 액세스 토큰을 사용할 수 있습니다. 참조 [Azure Active Directory를 사용 하 여](using-azure-active-directory.md) 자세한 정보에 대 한 합니다.

| 특성 값 | Description |
|-|-|
| NULL | (기본값) 액세스 토큰이 없는 제공 됩니다. |
| ACCESSTOKEN * | 액세스 토큰에 대 한 포인터입니다. |

### <a name="sqlcoptsscekeystoredata"></a>SQL_COPT_SS_CEKEYSTOREDATA

로드 된 키 저장소 공급자 라이브러리와 통신합니다. 컨트롤이 투명 한 열 암호화 (상시 암호화)를 참조 하십시오. 이 특성에 기본값이 없습니다. 참조 [사용자 지정 키 저장소 공급자](custom-keystore-providers.md) 자세한 정보에 대 한 합니다.

| 특성 값 | Description |
|-|-|
| CEKEYSTOREDATA * | Keystore 공급자 라이브러리에 대 한 통신 데이터 구조 |

### <a name="sqlcoptsscekeystoreprovider"></a>SQL_COPT_SS_CEKEYSTOREPROVIDER

상시 암호화를 위한 키 저장소 공급자 라이브러리를 로드 하거나 로드 된 키 저장소 공급자 라이브러리의 이름을 검색 합니다. 참조 [사용자 지정 키 저장소 공급자](custom-keystore-providers.md) 자세한 정보에 대 한 합니다. 이 특성에 기본값이 없습니다.

| 특성 값 | Description |
|-|-|
| char * | Keystore 공급자 라이브러리에 대 한 경로 |


