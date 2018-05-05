---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
caps.latest.revision: 60
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6419788b83a20dbfd1037be01723be23f1d277a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결 문자열 키워드를 대체하거나 개선하는 연결 특성을 정의합니다. 몇 가지 연결 문자열 키워드에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 지정한 기본값이 있습니다.  
  
 사용할 수 있는 키워드 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 참조 [Connection String Keywords with SQL Server Native Client를 사용 하 여](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)합니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 특성 및 드라이버 기본 동작 참조 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)합니다.  
  
 에 대 한 연결 문자열 키워드에 대해 유효한 설명은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client를 [Connection String Keywords with SQL Server Native Client를 사용 하 여](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)합니다.  
  
 경우는 **SQLDriverConnect * * * DriverCompletion* 매개 변수 값이 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED 이면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 키워드 값을 검색 하는 Native Client ODBC 드라이버는 표시 되는 대화 상자입니다. 키워드 값이 연결 문자열에서 전달되었고 사용자가 대화 상자에서 키워드 값을 변경하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결 문자열의 값을 사용합니다. 키워드 값이 연결 문자열에서 설정되지 않았고 사용자가 대화 상자에서 키워드 값을 지정하지 않은 경우 드라이버는 기본값을 사용합니다.  
  
 **SQLDriverConnect** 유효한 제공 해야 *WindowHandle* 경우 *DriverCompletion* 값 필요 (또는 채워야) 드라이버의 연결 대화 상자를 표시 합니다. 잘못된 핸들을 지정하면 SQL_ERROR가 반환됩니다.  
  
 DRIVER 또는 DSN 키워드 중 하나를 지정합니다. 둘 모두 지정한 경우 ODBC 드라이버는 이 두 키워드 중 왼쪽의 키워드를 사용하고 다른 하나는 무시합니다. 드라이버가 지정 되거나 둘 중에서 가장 왼쪽을 하는 경우와 **SQLDriverConnect * * * DriverCompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 이면 SERVER 키워드와 적절 한 값은 필수입니다.  
  
 SQL_DRIVER_NOPROMPT를 지정하는 경우에는 사용자 인증 키워드를 값과 함께 제공해야 합니다. 드라이버는 문자열 "Trusted_Connection=yes" 또는 UID와 PWD 키워드가 제공되었는지 확인합니다.  
  
 경우는 *DriverCompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED 및 언어나 데이터베이스 연결 문자열에서 가져오는데 고 하거나 유효 하지 않을 경우 **SQLDriverConnect**SQL_ERROR를 반환 합니다.  
  
 경우는 *DriverCompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED 언어나 데이터베이스 ODBC 데이터 원본 정의에서 제공 되 고 하거나 유효 하지 않을 경우 **SQLDriverConnect**  기본 언어나 데이터베이스를 사용 하 여 지정된 된 사용자 ID에 대 한 고 SQL_SUCCESS_WITH_INFO를 반환 합니다.  
  
 경우는 *DriverCompletion* 매개 변수 값이 SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_PROMPT이 고 언어나 데이터베이스 유효 인지 **SQLDriverConnect** 대화 상자를 다시 표시 합니다.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>고가용성 재해 복구를 위한 SQLDriverConnect 지원  
 사용에 대 한 자세한 내용은 **SQLDriverConnect** 에 연결 하는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 클러스터, 참조 [고가용성, 재해 복구에 대 한 SQL Server Native Client Support](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)합니다.  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>SPN(서비스 사용자 이름)에 대한 SQLDriverConnect 지원  
 SQLDDriverConnect은 ODBC 로그인 대화 상자 확인이 설정 된 사용 합니다. 이를 통해 주 서버 및 해당 장애 조치(Failover) 파트너 모두에 대한 SPN이 입력되도록 할 수 있습니다.  
  
 SQLDriverConnect 새 연결 문자열 키워드를 수락할 **ServerSPN** 및 **FailoverPartnerSPN**, 새 연결 특성인 SQL_COPT_SS_SERVER_SPN과 SQL_COPT_SS_를 인식 하 고 FAILOVER_PARTNER_SPN 합니다.  
  
 연결 특성 값이 두 번 이상 지정된 경우 프로그래밍 방식으로 설정된 값이 DSN의 값 및 연결 문자열의 값보다 우선 순위가 높고 DSN의 값이 연결 문자열의 값보다 우선 순위가 높습니다.  
  
 연결이 열릴 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 및 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD를 연결을 여는 데 사용하는 인증 방법으로 설정합니다.  
  
 Spn에 대 한 자세한 내용은 참조 [서비스 사용자 이름 & #40; Spn & #41; 클라이언트 연결 & #40; ODBC & #41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="examples"></a>예  
 다음 호출에서는 최소한에 필요한 데이터의 **SQLDriverConnect**:  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 다음 연결 문자열에 필요한 최소한의 데이터 설명 때는 *DriverCompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT:  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQLDriverConnect 함수](http://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
