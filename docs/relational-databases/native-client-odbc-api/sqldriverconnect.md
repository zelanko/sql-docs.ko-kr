---
title: SQL드라이버커넥트 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d1455f0b91313ea137ec9c13a2d318fba0807b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302554"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결 문자열 키워드를 대체하거나 개선하는 연결 특성을 정의합니다. 몇 가지 연결 문자열 키워드에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 지정한 기본값이 있습니다.  
  
 네이티브 클라이언트 ODBC 드라이버에서 사용할 수 있는 키워드 목록은 [SQL Server 네이티브 클라이언트와 연결 문자열 키워드 사용을](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)참조하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 연결 특성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 드라이버 기본 동작에 대한 자세한 내용은 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)을 참조하십시오.  
  
 네이티브 클라이언트에 유효한 연결 문자열 키워드에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설명은 SQL Server 네이티브 [클라이언트와 연결 문자열 키워드 사용을](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)참조하십시오.  
  
 **SQLDriverConnect**_드라이버완성_ 매개 변수 값이 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL_DRIVER_COMPLETE_REQUIRED 경우 네이티브 클라이언트 ODBC 드라이버는 표시된 대화 상자에서 키워드 값을 검색합니다. 키워드 값이 연결 문자열에서 전달되었고 사용자가 대화 상자에서 키워드 값을 변경하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결 문자열의 값을 사용합니다. 키워드 값이 연결 문자열에서 설정되지 않았고 사용자가 대화 상자에서 키워드 값을 지정하지 않은 경우 드라이버는 기본값을 사용합니다.  
  
 **SQLDriverConnect는** *드라이버완성* 값이 드라이버의 연결 대화 상자표시를 필요로 하거나 필요할 수 있는 경우 유효한 *WindowHandle을* 제공해야 합니다. 잘못된 핸들을 지정하면 SQL_ERROR가 반환됩니다.  
  
 DRIVER 또는 DSN 키워드 중 하나를 지정합니다. 둘 모두 지정한 경우 ODBC 드라이버는 이 두 키워드 중 왼쪽의 키워드를 사용하고 다른 하나는 무시합니다. DRIVER가 지정되거나 둘 중 가장 왼쪽이고 **SQLDriverConnect**_드라이버완성_ 매개 변수 값이 SQL_DRIVER_NOPROMPT 경우 SERVER 키워드와 적절한 값이 필요합니다.  
  
 SQL_DRIVER_NOPROMPT를 지정하는 경우에는 사용자 인증 키워드를 값과 함께 제공해야 합니다. 드라이버는 문자열 "Trusted_Connection=yes" 또는 UID와 PWD 키워드가 제공되었는지 확인합니다.  
  
 *DriverCompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED 언어 또는 데이터베이스가 연결 문자열에서 가져오고 둘 중 하나가 유효하지 않은 경우 **SQLDriverConnect는** SQL_ERROR 반환합니다.  
  
 *DriverCompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED 및 언어 또는 데이터베이스ODBC 데이터 원본 정의에서 가져오고 잘못 된 경우 **SQLDriverConnect** 지정된 된 사용자 ID에 대 한 기본 언어 또는 데이터베이스를 사용 하 고 SQL_SUCCESS_WITH_INFO 반환 합니다.  
  
 *Driver완성* 매개 변수 값이 SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_PROMPT 언어 또는 데이터베이스가 잘못되면 **SQLDriverConnect에서** 대화 상자를 다시 표시합니다.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>고가용성 재해 복구를 위한 SQLDriverConnect 지원  
 클러스터에 연결하기 위해 **SQLDriverConnect를** 사용하는 것에 대한 자세한 내용은 [고가용성, 재해 복구에 대한 SQL Server 네이티브 클라이언트 지원을](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)참조하십시오. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>SPN(서비스 사용자 이름)에 대한 SQLDriverConnect 지원  
 SQLDDriverConnect는 메시지가 활성화되면 ODBC 로그인 대화 상자상자를 사용합니다. 이를 통해 주 서버 및 해당 장애 조치(Failover) 파트너 모두에 대한 SPN이 입력되도록 할 수 있습니다.  
  
 SQLDriverConnect는 새 연결 문자열 키워드 **인 ServerSPN** 및 **FailoverPartnerSPN을**수락하고 SQL_COPT_SS_SERVER_SPN 새 연결 특성을 인식하고 SQL_COPT_SS_FAILOVER_PARTNER_SPN.  
  
 연결 특성 값이 두 번 이상 지정된 경우 프로그래밍 방식으로 설정된 값이 DSN의 값 및 연결 문자열의 값보다 우선 순위가 높고 DSN의 값이 연결 문자열의 값보다 우선 순위가 높습니다.  
  
 연결이 열릴 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 및 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD를 연결을 여는 데 사용하는 인증 방법으로 설정합니다.  
  
 SP에 대한 자세한 내용은 [ODBC&#41;클라이언트 &#40;연결에서&#41; &#40;서비스 주체 이름을 ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)참조하십시오.  
  
## <a name="examples"></a>예  
 다음 호출은 **SQLDriverConnect에**필요한 최소한의 데이터를 보여 줍니다.  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 다음 연결 문자열은 *DriverCompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 때 최소 필요한 데이터를 보여 줍니다.  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL드라이버연결 기능](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 구현 세부 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [&#40;거래 SQL&#41;ANSI_NULLS 설정](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [&#40;거래 SQL&#41;ANSI_PADDING 설정](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
