---
title: SQLSetConnectAttr | Microsoft Docs
description: SQL Server Native Client ODBC 드라이버에서 설정 된 값과 가능한 값을 포함 하 여 SQLSetConnectAttr의 연결 특성에 대해 알아봅니다.
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetConnectAttr function
ms.assetid: d21b5cf1-3724-43f7-bc96-5097df0677b4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b3c006da487774a8de01ccf9a9b8cd12d9ca15f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465124"
---
# <a name="sqlsetconnectattr"></a>SQLSetConnectAttr

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 SQL_ATTR_CONNECTION_TIMEOUT의 설정을 무시합니다.  
  
 SQL_ATTR_TRANSLATE_LIB도 무시됩니다. 다른 변환 라이브러리는 지정할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 Microsoft ODBC 드라이버를 사용하도록 애플리케이션을 쉽게 옮길 수 있게 하기 위해 SQL_ATTR_TRANSLATE_LIB를 사용하여 설정한 값은 모두 드라이버 관리자의 버퍼를 거쳐 복사됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 반복 읽기 트랜잭션 격리를 직렬화 가능하도록 구현합니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에는 새로운 트랜잭션 격리 특성인 SQL_COPT_SS_TXN_ISOLATION이 지원됩니다. SQL_COPT_SS_TXN_ISOLATION을 SQL_TXN_SS_SNAPSHOT으로 설정하면 스냅샷 격리 수준에서 트랜잭션이 실행됩니다.  
  
> [!NOTE]  
> SQL_ATTR_TXN_ISOLATION을 사용하면 SQL_TXN_SS_SNAPSHOT을 제외한 다른 모든 격리 수준을 설정할 수 있습니다. 스냅샷 격리를 사용하려면 SQL_COPT_SS_TXN_ISOLATION을 통해 SQL_TXN_SS_SNAPSHOT을 설정해야 합니다. 그러나 격리 수준을 검색할 때는 SQL_ATTR_TXN_ISOLATION이나 SQL_COPT_SS_TXN_ISOLATION을 모두 사용할 수 있습니다.  
  
 ODBC 문 특성을 연결 특성으로 승격하면 예기치 않은 결과가 발생할 수 있습니다. 결과 집합 처리를 위해 서버 커서를 요청하는 문 특성은 연결로 승격할 수 있습니다. 예를 들어 ODBC 문 특성 SQL_ATTR_CONCURRENCY를 기본 SQL_CONCUR_READ_ONLY보다 더 제한적인 값으로 설정하면 드라이버는 연결을 통해 전송한 모든 문에 대해 동적 커서를 사용합니다. 연결을 통해 문에 ODBC 카탈로그 함수를 실행하면 SQL_SUCCESS_WITH_INFO 및 커서 동작이 읽기 전용으로 변경되었음을 나타내는 진단 레코드가 반환됩니다. 같은 연결에서 COMPUTE 절이 포함된 Transact-SQL SELECT 문을 실행하려고 하면 문 실행이 실패합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 sqlncli.h에 정의되어 있는 ODBC 연결 특성에 대해 여러 가지 드라이버별 확장을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용할 경우 연결하기 전에 특성을 설정해야 하거나, 특성이 이미 설정되어 있는 경우 해당 특성이 무시될 수 있습니다. 다음 표에서는 제한을 나열합니다.  
  
|SQL Server 특성|설정 시점(서버 연결 이전 또는 이후)|  
|--------------------------|----------------------------------------------|  
|SQL_COPT_SS_ANSI_NPW|이전|  
|SQL_COPT_SS_APPLICATION_INTENT|이전|  
|SQL_COPT_SS_ATTACHDBFILENAME|이전|  
|SQL_COPT_SS_BCP|이전|  
|SQL_COPT_SS_BROWSE_CONNECT|이전|  
|SQL_COPT_SS_BROWSE_SERVER|이전|  
|SQL_COPT_SS_CONCAT_NULL|이전|  
|SQL_COPT_SS_CONNECTION_DEAD|이러한|  
|SQL_COPT_SS_ENCRYPT|이전|  
|SQL_COPT_SS_ENLIST_IN_DTC|이러한|  
|SQL_COPT_SS_ENLIST_IN_XA|이러한|  
|SQL_COPT_SS_FALLBACK_CONNECT|이전|  
|SQL_COPT_SS_FAILOVER_PARTNER|이전|  
|SQL_COPT_SS_INTEGRATED_SECURITY|이전|  
|SQL_COPT_SS_MARS_ENABLED|이전|  
|SQL_COPT_SS_MULTISUBNET_FAILOVER|이전|  
|SQL_COPT_SS_OLDPWD|이전|  
|SQL_COPT_SS_PERF_DATA|이러한|  
|SQL_COPT_SS_PERF_DATA_LOG|이러한|  
|SQL_COPT_SS_PERF_DATA_LOG_NOW|이러한|  
|SQL_COPT_SS_PERF_QUERY|이러한|  
|SQL_COPT_SS_PERF_QUERY_INTERVAL|이러한|  
|SQL_COPT_SS_PERF_QUERY_LOG|이러한|  
|SQL_COPT_SS_PRESERVE_CURSORS|이전|  
|SQL_COPT_SS_QUOTED_IDENT|여기서는|  
|SQL_COPT_SS_TRANSLATE|여기서는|  
|SQL_COPT_SS_TRUST_SERVER_CERTIFICATE|이전|  
|SQL_COPT_SS_TXN_ISOLATION|여기서는|  
|SQL_COPT_SS_USE_PROC_FOR_PREP|여기서는|  
|SQL_COPT_SS_USER_DATA|여기서는|  
|SQL_COPT_SS_WARN_ON_CP_ERROR|이전|  
  
 동일한 세션, 데이터베이스 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 상태에 대해 사전 연결 특성 및 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령을 사용하면 예기치 못한 동작이 발생할 수 있습니다. 예제:  
  
```  
SQLSetConnectAttr(SQL_COPT_SS_QUOTED_IDENT, SQL_QI_ON) // turn ON via attribute  
SQLDriverConnect(...);  
SQLExecDirect("SET QUOTED_IDENTIFIER OFF") // turn OFF via Transact-SQL  
SQLSetConnectAttr(SQL_ATTR_CURRENT_CATALOG, ...) // restores to pre-connect attribute value  
```  

<a name="sqlcoptssansinpw"></a>
## <a name="sql_copt_ss_ansi_npw"></a>SQL_COPT_SS_ANSI_NPW  
 SQL_COPT_SS_ANSI_NPW는 비교와 연결의 NULL, 문자 데이터 형식 패딩 및 경고에 ISO 처리를 사용하거나 사용하지 않도록 설정합니다. 자세한 내용은 SET ANSI_NULLS, SET ANSI_PADDING, SET ANSI_WARNINGS 및 SET CONCAT_NULL_YIELDS_NULL을 참조하십시오.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_AD_ON|기본값 연결에서 NULL 비교, 패딩, 경고 및 NULL 연결 처리에 ANSI 기본 동작을 사용합니다.|  
|SQL_AD_OFF|연결에서 NULL, 문자 데이터 형식 패딩 및 경고에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 정의된 처리 방식을 사용합니다.|  
  
 연결 풀링을 사용 하는 경우 SQLSetConnectAttr를 사용 하는 대신 연결 문자열에 SQL_COPT_SS_ANSI_NPW를 설정 해야 합니다. 연결 풀링을 사용할 경우 연결이 설정된 후 이 특성을 변경하려고 시도하면 자동으로 실패합니다.  

<a name="sqlcoptssapplicationintent"></a>
## <a name="sql_copt_ss_application_intent"></a>SQL_COPT_SS_APPLICATION_INTENT  
 서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 가능한 값은 **Readonly** 및 **ReadWrite** 입니다. 예를 들어:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_APPLICATION_INTENT, TEXT("Readonly"), SQL_NTS)  
```  
  
 기본값은 **ReadWrite** 입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client의 ag 지원에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] [고가용성, 재해 복구를 위한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)을 참조 하세요.  

<a name="sqlcoptssattachdbfilename"></a>
## <a name="sql_copt_ss_attachdbfilename"></a>SQL_COPT_SS_ATTACHDBFILENAME  
 SQL_COPT_SS_ATTACHDBFILENAME은 연결할 수 있는 데이터베이스의 주 파일 이름을 지정합니다. 이 데이터베이스는 연결되어 해당 연결에 대한 기본 데이터베이스가 됩니다. SQL_COPT_SS_ATTACHDBFILENAME를 사용 하려면 데이터베이스의 이름을 connection 특성 SQL_ATTR_CURRENT_CATALOG 값으로 지정 하거나 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)의 database = 매개 변수에 지정 해야 합니다. 데이터베이스가 이전에 연결된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 데이터베이스를 다시 연결하지 않습니다.  
  
|값|설명|  
|-----------|-----------------|  
|문자열에 대한 SQLPOINTER|연결할 데이터베이스의 주 파일 이름이 문자열에 포함됩니다. 파일의 전체 경로 이름을 포함해야 합니다.|  

<a name="sqlcoptssbcp"></a>
## <a name="sql_copt_ss_bcp"></a>SQL_COPT_SS_BCP  
 SQL_COPT_SS_BCP를 사용하면 연결에서 대량 복사 함수를 사용할 수 있습니다. 자세한 내용은 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)를 참조 하세요.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_BCP_OFF|기본값 연결에서 대량 복사 함수를 사용할 수 없습니다.|  
|SQL_BCP_ON|연결에서 대량 복사 함수를 사용할 수 있습니다.|  

<a name="sqlcoptssbrowseconnect"></a>
## <a name="sql_copt_ss_browse_connect"></a>SQL_COPT_SS_BROWSE_CONNECT  
 이 특성은 [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)에서 반환 된 결과 집합을 사용자 지정 하는 데 사용 됩니다. SQL_COPT_SS_BROWSE_CONNECT를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 열거된 인스턴스에서 추가적인 정보를 반환하거나 반환하지 않도록 설정합니다. 추가적인 정보에는 서버가 클러스터인지 여부, 여러 인스턴스의 이름 및 버전 번호가 포함됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_MORE_INFO_NO|기본값 서버 목록을 반환합니다.|  
|SQL_MORE_INFO_YES|**SQLBrowseConnect** 는 서버 속성의 확장 문자열을 반환 합니다.|  

<a name="sqlcoptssbrowseserver"></a>
## <a name="sql_copt_ss_browse_server"></a>SQL_COPT_SS_BROWSE_SERVER  
 이 특성은 **SQLBrowseConnect** 에서 반환 된 결과 집합을 사용자 지정 하는 데 사용 됩니다. SQL_COPT_SS_BROWSE_SERVER **SQLBrowseConnect** 정보를 반환 하는 서버 이름을 지정 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|컴퓨터 이름|**SQLBrowseConnect** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 된 컴퓨터에 있는 인스턴스 목록을 반환 합니다. \\ \\ 서버 이름에는 이중 백슬래시 ()를 사용 하지 않아야 합니다. 예를 들어 \\ \Myserver, MyServer를 사용 해야 합니다.|  
|NULL|기본값 **SQLBrowseConnect** 는 도메인에 있는 모든 서버에 대 한 정보를 반환 합니다.|  

<a name="sqlcoptssconcatnull"></a>
## <a name="sql_copt_ss_concat_null"></a>SQL_COPT_SS_CONCAT_NULL  
 SQL_COPT_SS_CONCAT_NULL은 문자열을 연결할 때 NULL에 대해 ISO 처리를 사용하거나 사용하지 않도록 설정합니다. 자세한 내용은 SET CONCAT_NULL_YIELDS_NULL을 참조하십시오.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_CN_ON|기본값 연결에서 문자열을 연결할 때 ISO 기본값을 사용하여 NULL 값을 처리합니다.|  
|SQL_CN_OFF|연결에서 문자열을 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 정의된 동작을 사용하여 NULL 값을 처리합니다.|  

<a name="sqlcoptssencrypt"></a>
## <a name="sql_copt_ss_encrypt"></a>SQL_COPT_SS_ENCRYPT  
 연결의 암호화를 제어합니다.  
  
 암호화에는 서버에 있는 인증서가 사용됩니다. 이 인증서는 연결 특성 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE를 SQL_TRUST_SERVER_CERTIFICATE_YES로 설정하거나 연결 문자열에 "TrustServerCertificate=yes"가 포함된 경우를 제외하고는 인증 기관에서 확인된 인증서여야 합니다. 이 두 조건 중 하나에 해당하는 경우 서버에 인증서가 없으면 서버에서 생성되고 서명된 인증서를 사용하여 연결을 암호화할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_EN_ON|연결을 암호화합니다.|  
|SQL_EN_OFF|연결을 암호화하지 않습니다. 이것이 기본값입니다.|  

<a name="sqlcoptssenlistindtc"></a>
## <a name="sql_copt_ss_enlist_in_dtc"></a>SQL_COPT_SS_ENLIST_IN_DTC  
 클라이언트는 ms dtc (Microsoft DTC(Distributed Transaction Coordinator)) OLE DB **ITransactionDispenser:: BeginTransaction** 메서드를 호출 하 여 ms dtc 트랜잭션을 시작 하 고 해당 트랜잭션을 나타내는 ms dtc 트랜잭션 개체를 만듭니다. 그런 다음 응용 프로그램은 SQL_COPT_SS_ENLIST_IN_DTC 옵션을 사용 하 여 **SQLSetConnectAttr** 을 호출 하 여 트랜잭션 개체를 ODBC 연결과 연결 합니다. 관련된 모든 데이터베이스 작업은 MS DTC 트랜잭션의 보호 아래 수행됩니다. 응용 프로그램은 SQL_DTC_DONE를 사용 하 여 **SQLSetConnectAttr** 를 호출 하 여 연결의 DTC 연결을 종료 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|DTC 개체*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 내보낼 트랜잭션을 지정하는 MS DTC OLE 트랜잭션 개체입니다.|  
|SQL_DTC_DONE|DTC 트랜잭션의 종료를 구분합니다.|  

<a name="sqlcoptssenlistinxa"></a>
## <a name="sql_copt_ss_enlist_in_xa"></a>SQL_COPT_SS_ENLIST_IN_XA  
 XA 호환 트랜잭션 프로세서 (TP)를 사용 하 여 XA 트랜잭션을 시작 하기 위해 클라이언트는 Open Group **tx_begin** 함수를 호출 합니다. 그런 다음 응용 프로그램은 SQL_COPT_SS_ENLIST_IN_XA 매개 변수가 TRUE 인 **SQLSetConnectAttr** 를 호출 하 여 XA 트랜잭션을 ODBC 연결과 연결 합니다. 관련된 모든 데이터베이스 작업은 XA 트랜잭션의 보호 아래 수행됩니다. ODBC 연결을 사용 하 여 XA 연결을 종료 하려면 클라이언트는 SQL_COPT_SS_ENLIST_IN_XA 매개 변수를 FALSE로 설정 하 여 **SQLSetConnectAttr** 를 호출 해야 합니다. 자세한 내용은 Microsoft Distributed Transaction Coordinator 설명서를 참조하십시오.  
  
## <a name="sql_copt_ss_fallback_connect"></a>SQL_COPT_SS_FALLBACK_CONNECT  
 이 특성은 더 이상 지원되지 않습니다.  

<a name="sqlcoptssfailoverpartner"></a>
## <a name="sql_copt_ss_failover_partner"></a>SQL_COPT_SS_FAILOVER_PARTNER  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 미러링에 사용되는 장애 조치(failover) 파트너의 이름을 지정하거나 검색하는 데 사용되며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 처음 연결하기 전에 설정해야 하는 Null로 끝나는 문자열입니다.  
  
 연결한 후 응용 프로그램은 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 를 사용 하 여이 특성을 쿼리하여 장애 조치 (failover) 파트너의 id를 확인할 수 있습니다. 주 서버에 장애 조치(failover) 파트너가 없는 경우 이 속성은 빈 문자열을 반환합니다. 이를 통해 지능형 애플리케이션은 가장 최근에 확인된 백업 서버를 캐시할 수 있지만 이러한 애플리케이션은 연결이 처음 설정될 때(또는 풀링된 경우 다시 설정될 때)만 정보가 업데이트되므로 장시간 연결에서는 정보가 최신 상태가 아닐 수 있음에 주의해야 합니다.  
  
 자세한 내용은 [데이터베이스 미러링 사용](../../relational-databases/native-client/features/using-database-mirroring.md)을 참조하세요.  

<a name="sqlcoptssintegratedsecurity"></a>
## <a name="sql_copt_ss_integrated_security"></a>SQL_COPT_SS_INTEGRATED_SECURITY  
 SQL_COPT_SS_INTEGRATED_SECURITY를 사용하면 서버 로그인 시 액세스를 확인하는 데 Windows 인증이 사용됩니다. Windows 인증을 사용 하는 경우 드라이버는 **SQLConnect**, [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)또는 [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) processing의 일부로 제공 된 사용자 식별자 및 암호 값을 무시 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_IS_OFF|기본값 로그인 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 사용자 식별자와 암호를 확인합니다.|  
|SQL_IS_ON|Windows 인증 모드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 사용자의 액세스 권한을 확인합니다.|  

<a name="sqlcoptssmarsenabled"></a>
## <a name="sql_copt_ss_mars_enabled"></a>SQL_COPT_SS_MARS_ENABLED  
 이 특성은 MARS(Multiple Active Result Sets)를 사용하거나 사용하지 않도록 설정합니다. 기본적으로 MARS는 사용되지 않습니다. 이 특성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하기 전에 설정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결된 후 MARS는 연결의 유효 기간 동안 설정되거나 설정되지 않은 상태로 유지됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_MARS_ENABLED_NO|기본값 MARS(Multiple Active Result Sets)를 사용하지 않습니다.|  
|SQL_MARS_ENABLED_YES|MARS를 사용합니다.|  
  
 MARS에 대 한 자세한 내용은 [mars&#41;&#40;여러 활성 결과 집합 사용 ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조 하세요.  

<a name="sqlcoptssmultisubnetfailover"></a>
## <a name="sql_copt_ss_multisubnet_failover"></a>SQL_COPT_SS_MULTISUBNET_FAILOVER  
 애플리케이션이 다른 서브넷에 있는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] AG(가용성 그룹)에 연결하는 경우 이 연결 속성을 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 현재 활성 서버를 보다 빠르게 검색하고 연결할 수 있도록 구성됩니다. 예를 들어:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MULTISUBNET_FAILOVER, SQL_IS_ON, SQL_IS_INTEGER)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client의 ag 지원에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] [고가용성, 재해 복구를 위한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)을 참조 하세요.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_IS_ON|장애 조치(failover)가 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서는 보다 빠른 재연결을 제공합니다.|  
|SQL_IS_OFF|장애 조치(failover)가 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서는 보다 빠른 재연결을 제공하지 않습니다.|  

<a name="sqlcoptssoldpwd"></a>
## <a name="sql_copt_ss_oldpwd"></a>SQL_COPT_SS_OLDPWD  
 SQL Server 인증의 암호 만료가 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 도입되었습니다. SQL_COPT_SS_OLDPWD 특성은 클라이언트에서 이전 연결 암호와 새 연결 암호를 모두 제공할 수 있도록 추가되었습니다. 이 속성을 설정하면 변경된 "이전 암호"가 연결 문자열에 포함되기 때문에 공급자가 첫 번째 연결 또는 이후 연결에 연결 풀을 사용하지 않습니다.  
  
 자세한 내용은 [프로그래밍 방식으로 암호 변경](../../relational-databases/native-client/features/changing-passwords-programmatically.md)을 참조하세요.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_COPT_SS_OLD_PASSWORD|이전 암호가 포함된 문자열에 대한 SQLPOINTER입니다. 이 값은 쓰기 전용이며 서버에 연결하기 전에 설정해야 합니다.|  

<a name="sqlcoptssperfdata"></a>
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA는 성능 데이터 로깅을 시작하거나 중지합니다. 데이터 로그 파일 이름은 데이터 로깅을 시작하기 전에 설정해야 합니다. 아래의 SQL_COPT_SS_PERF_DATA_LOG를 참조하십시오.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_PERF_START|성능 데이터를 샘플링하는 드라이버를 시작합니다.|  
|SQL_PERF_STOP|카운터의 성능 데이터 샘플링을 중지합니다.|  
  
 자세한 내용은 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)를 참조 하세요.  

<a name="sqlcoptssperfdatalog"></a>
## <a name="sql_copt_ss_perf_data_log"></a>SQL_COPT_SS_PERF_DATA_LOG  
 SQL_COPT_SS_PERF_DATA_LOG는 성능 데이터를 기록하는 데 사용되는 로그 파일의 이름을 할당합니다. 로그 파일 이름은 애플리케이션 컴파일 방식에 따라 Null로 끝나는 ANSI 또는 유니코드 문자열입니다. *Stringlength* 인수는 SQL_NTS 이어야 합니다.  

<a name="sqlcoptssperfdatalognow"></a>
## <a name="sql_copt_ss_perf_data_log_now"></a>SQL_COPT_SS_PERF_DATA_LOG_NOW  
 SQL_COPT_SS_PERF_DATA_LOG_NOW는 통계 로그 항목을 디스크에 쓰도록 드라이버에 지시합니다. *Stringlength* 인수는 SQL_NTS 이어야 합니다.  

<a name="sqlcoptssperfquery"></a>
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 SQL_COPT_SS_PERF_QUERY는 장기 실행 쿼리에 대한 로깅을 시작하거나 중지합니다. 쿼리 로그 파일 이름은 로깅을 시작하기 전에 지정해야 합니다. 애플리케이션에서는 로깅 간격을 설정하여 &quot;장기 실행&quot;을 정의할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_PERF_START|장기 실행 쿼리의 로깅을 시작합니다.|  
|SQL_PERF_STOP|장기 실행 쿼리의 로깅을 중지합니다.|  
  
 자세한 내용은 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)를 참조 하세요.  

<a name="sqlcoptssperfqueryinterval"></a>
## <a name="sql_copt_ss_perf_query_interval"></a>SQL_COPT_SS_PERF_QUERY_INTERVAL  
 SQL_COPT_SS_PERF_QUERY_INTERVAL은 쿼리 로깅 임계값을 밀리초 단위로 설정합니다. 지정된 임계값 내에 확인되지 않는 쿼리는 장기 실행 쿼리 로그 파일에 기록됩니다. 쿼리 임계값에는 상한값이 없으며 쿼리 임계값이 0이면 모든 쿼리가 로깅됩니다.  

<a name="sqlcoptssperfquerylog"></a>
## <a name="sql_copt_ss_perf_query_log"></a>SQL_COPT_SS_PERF_QUERY_LOG  
 SQL_COPT_SS_PERF_QUERY_LOG는 장기 실행 쿼리 데이터를 기록할 로그 파일의 이름을 할당합니다. 로그 파일 이름은 애플리케이션 컴파일 방식에 따라 Null로 끝나는 ANSI 또는 유니코드 문자열입니다. *Stringlength* 인수는 SQL_NTS 또는 문자열의 길이 (바이트) 여야 합니다.  

<a name="sqlcoptsspreservecursors"></a>
## <a name="sql_copt_ss_preserve_cursors"></a>SQL_COPT_SS_PRESERVE_CURSORS  
 이 특성을 사용하면 트랜잭션을 커밋/롤백할 때 연결에 커서를 유지할지 여부를 설정하고 쿼리할 수 있습니다. SQL_PC_ON 또는 SQL_PC_OFF로 설정할 수 있으며 기본값은 SQL_PC_OFF입니다. 이 설정은 [Sqlendtran](../../relational-databases/native-client-odbc-api/sqlendtran.md) (또는 sqltransact-sql)를 호출할 때 드라이버가 커서를 닫을지 여부를 제어 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_PC_OFF|기본값 **Sqlendtran** 을 사용 하 여 트랜잭션을 커밋하거나 롤백할 때 커서가 닫힙니다.|  
|SQL_PC_ON|비동기 모드에서 정적 또는 키 집합 커서를 사용 하는 경우를 제외 하 고 **Sqlendtran** 을 사용 하 여 트랜잭션을 커밋하거나 롤백하는 경우에는 커서가 닫히지 않습니다. 커서가 완전하게 채워지지 않은 상태에서 롤백을 실행하면 커서가 닫힙니다.|  

<a name="sqlcoptssquotedident"></a>
## <a name="sql_copt_ss_quoted_ident"></a>SQL_COPT_SS_QUOTED_IDENT  
 SQL_COPT_SS_QUOTED_IDENT를 사용하면 연결에서 전송하는 ODBC 및 Transact-SQL 문에 따옴표 붙은 식별자를 사용할 수 있습니다. 따옴표 붙은 식별자를 제공하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 식별자에 공백 문자가 들어 있어 원래는 올바르지 않은 "My Table" 같은 개체 이름을 사용할 수 있습니다. 자세한 내용은 SET QUOTED_IDENTIFIER를 참조하십시오.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_QI_OFF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에서 전송하는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 따옴표 붙은 식별자를 사용할 수 없습니다.|  
|SQL_QI_ON|기본값 연결에서 전송하는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 따옴표 붙은 식별자를 사용할 수 있습니다.|  

<a name="sqlcoptsstranslate"></a>
## <a name="sql_copt_ss_translate"></a>SQL_COPT_SS_TRANSLATE  
 SQL_COPT_SS_TRANSLATE를 설정하면 MBCS 데이터를 교환할 때 드라이버가 클라이언트와 서버 코드 페이지 간에 문자를 변환합니다. 특성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char**, **varchar** 및 **text** 열에 저장 된 데이터에만 영향을 줍니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_XL_OFF|드라이버가 클라이언트와 서버 사이에 교환되는 문자 데이터에서 코드 페이지의 문자를 다른 문자로 변환하지 않습니다.|  
|SQL_XL_ON|기본값 드라이버가 클라이언트와 서버 사이에 교환되는 문자 데이터에서 코드 페이지의 문자를 다른 문자로 변환합니다. 드라이버는 문자 변환을 자동으로 구성하여 서버에 설치된 코드 페이지와 클라이언트에서 사용하는 코드 페이지를 확인합니다.|  

<a name="sqlcoptsstrustservercertificate"></a>
## <a name="sql_copt_ss_trust_server_certificate"></a>SQL_COPT_SS_TRUST_SERVER_CERTIFICATE  
 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE를 사용하면 암호화를 사용할 때 드라이버가 인증서를 확인하거나 확인하지 않도록 설정합니다. 이 특성은 읽기/쓰기 값이지만 연결이 설정된 후에 설정하면 아무 효과가 없습니다.  
  
 클라이언트 애플리케이션은 연결이 열린 후에 이 속성을 쿼리하여 실제 사용되는 암호화 및 유효성 검사 설정을 확인할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_TRUST_SERVER_CERTIFICATE_NO|기본값 인증서 확인 없는 암호화를 사용할 수 없습니다.|  
|SQL_TRUST_SERVER_CERTIFICATE_YES|인증서 확인 없는 암호화를 사용할 수 있습니다.|  

<a name="sqlcoptsstxnisolation"></a>
## <a name="sql_copt_ss_txn_isolation"></a>SQL_COPT_SS_TXN_ISOLATION  
 SQL_COPT_SS_TXN_ISOLATION은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]별 스냅샷 격리 특성을 설정합니다. 이 경우 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 따라 다르기 때문에 SQL_ATTR_TXN_ISOLATION을 사용하여 스냅샷 격리를 설정할 수 없습니다. 그러나 스냅숏 격리를 검색할 때는 SQL_ATTR_TXN_ISOLATION 또는 SQL_COPT_SS_TXN_ISOLATION을 사용할 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_TXN_SS_SNAPSHOT|트랜잭션에서 다른 트랜잭션의 변경 내용을 볼 수 없고 다시 쿼리하는 경우에도 변경 내용을 볼 수 없음을 나타냅니다.|  
  
 스냅숏 격리에 대 한 자세한 내용은 [Snapshot 격리 작업](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)을 참조 하세요.  
  
## <a name="sql_copt_ss_use_proc_for_prep"></a>SQL_COPT_SS_USE_PROC_FOR_PREP

 이 특성은 더 이상 지원되지 않습니다.  

<a name="sqlcoptssuserdata"></a>
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA는 사용자 데이터 포인터를 설정합니다. 사용자 데이터는 연결별로 기록되는 클라이언트 소유의 메모리입니다.  
  
 자세한 내용은 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)를 참조 하세요.  

<a name="sqlcoptsswarnoncperror"></a>
## <a name="sql_copt_ss_warn_on_cp_error"></a>SQL_COPT_SS_WARN_ON_CP_ERROR  
 이 특성은 코드 페이지 변환 중에 데이터가 손실될 경우 경고를 표시할지 여부를 결정합니다. 이 특성은 서버에서 들어오는 데이터에만 적용됩니다.  
  
|값|설명|  
|-----------|-----------------|  
|SQL_WARN_YES|코드 페이지 변환 중에 데이터 손실이 발생할 경우 경고를 생성합니다.|  
|SQL_WARN_NO|(기본값) 코드 페이지 변환 중에 데이터 손실이 발생할 경우 경고를 생성하지 않습니다.|  
  
## <a name="sqlsetconnectattr-support-for-service-principal-names-spns"></a>SPN에 대한 SQLSetConnectAttr 지원

 SQLSetConnectAttr를 사용 하 여 SQL_COPT_SS_SERVER_SPN 새 연결 특성의 값을 설정 하 고 SQL_COPT_SS_FAILOVER_PARTNER_SPN 수 있습니다. 이러한 특성은 연결이 열려 있는 상태에서는 설정할 수 없습니다. 연결이 열려 있을 때 이러한 특성을 설정하려고 하면 "작업을 현재 사용할 수 없습니다."라는 메시지와 함께 HY011 오류가 반환됩니다. SQLSetConnectOption를 사용 하 여 이러한 값을 설정할 수도 있습니다.  
  
 Spn에 대 한 자세한 내용은 [클라이언트 연결 &#40;ODBC&#41;에서 spn&#41; &#40;서비스 사용자 이름 ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)을 참조 하세요.  

<a name="sqlcoptssconnectiondead"></a>
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 이 특성은 읽기 전용입니다.  
  
 SQL_COPT_SS_CONNECTION_DEAD에 대 한 자세한 내용은 [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) and [To a DATA Source &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)을 참조 하십시오.  
  
## <a name="example"></a>예

 이 예에서는 성능 데이터를 로깅합니다.  
  
```  
SQLPERF*     pSQLPERF;  
SQLINTEGER   nValue;  
  
// See if you are already logging. SQLPERF* will be NULL if not.  
SQLGetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA, &pSQLPERF,  
    sizeof(SQLPERF*), &nValue);  
  
if (pSQLPERF == NULL)  
    {  
    // Set the performance log file name.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG,  
        (SQLPOINTER) "\\My LogDirectory\\MyServerLog.txt", SQL_NTS);  
  
    // Start logging...  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
        (SQLPOINTER) SQL_PERF_START, SQL_IS_INTEGER);  
    }  
else  
    {  
    // Take a snapshot now so that your performance statistics are discernible.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
    }  
  
    // ...perform some action...  
  
// ...take a performance data snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
    // ...perform more actions...  
  
// ...take another snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
// ...and disable logging.  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
    (SQLPOINTER) SQL_PERF_STOP, SQL_IS_INTEGER);  
  
// Continue on...  
```  
  
## <a name="see-also"></a>참고 항목

 [SQLSetConnectAttr 함수](../../odbc/reference/syntax/sqlsetconnectattr-function.md)   
 [ODBC API 구현 세부 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)   
 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SQLPrepare 함수](../../odbc/reference/syntax/sqlprepare-function.md)   
 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)  
  
