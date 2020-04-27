---
title: SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22d560c8a65d5b9a7cebc4062ddd2d1ce936d5a2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067749"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결 문자열 키워드를 대체하거나 개선하는 연결 특성을 정의합니다. 몇 가지 연결 문자열 키워드에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 지정한 기본값이 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버에서 사용할 수 있는 키워드 목록은 [SQL Server Native Client와 연결 문자열 키워드 사용](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조 하세요.  
  
 연결 특성 및 드라이버 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 동작에 대 한 자세한 내용은 [SQLSetConnectAttr](sqlsetconnectattr.md)를 참조 하세요.  
  
 Native Client에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유효한 연결 문자열 키워드에 대 한 설명은 [SQL Server Native Client 연결 문자열 키워드 사용](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조 하세요.  
  
 `SQLDriverConnect` *Drivercompletion* 매개 변수 값이 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_COMPLETE_REQUIRED 인 경우 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버는 표시 된 대화 상자에서 키워드 값을 검색 합니다. 키워드 값이 연결 문자열에서 전달되었고 사용자가 대화 상자에서 키워드 값을 변경하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 연결 문자열의 값을 사용합니다. 키워드 값이 연결 문자열에서 설정되지 않았고 사용자가 대화 상자에서 키워드 값을 지정하지 않은 경우 드라이버는 기본값을 사용합니다.  
  
 `SQLDriverConnect`*Drivercompletion* 값에는 드라이버의 연결 대화 상자를 표시 해야 하거나 필요한 경우 올바른 *WindowHandle* 를 제공 해야 합니다. 잘못된 핸들을 지정하면 SQL_ERROR가 반환됩니다.  
  
 DRIVER 또는 DSN 키워드 중 하나를 지정합니다. 둘 모두 지정한 경우 ODBC 드라이버는 이 두 키워드 중 왼쪽의 키워드를 사용하고 다른 하나는 무시합니다. 드라이버가 지정 된 경우 또는이 둘 중 가장 왼쪽 이며 `SQLDriverConnect` *drivercompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 이면 서버 키워드와 적절 한 값이 필요 합니다.  
  
 SQL_DRIVER_NOPROMPT를 지정하는 경우에는 사용자 인증 키워드를 값과 함께 제공해야 합니다. 드라이버는 문자열 "Trusted_Connection=yes" 또는 UID와 PWD 키워드가 제공되었는지 확인합니다.  
  
 *Drivercompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED이 고 언어 또는 데이터베이스가 연결 문자열에서 제공 되 고가 유효 하지 않은 경우 `SQLDriverConnect` 는 SQL_ERROR을 반환 합니다.  
  
 *Drivercompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 또는 SQL_DRIVER_COMPLETE_REQUIRED이 고 언어나 데이터베이스가 ODBC 데이터 원본 정의에서 제공 되 고 잘못 된 경우는 지정 된 `SQLDriverConnect` 사용자 ID에 대해 기본 언어나 데이터베이스를 사용 하 고 SQL_SUCCESS_WITH_INFO을 반환 합니다.  
  
 *Drivercompletion* 매개 변수 값이 SQL_DRIVER_COMPLETE 또는 SQL_DRIVER_PROMPT이 고 언어나 데이터베이스가 잘못 된 경우 대화 상자를 `SQLDriverConnect` 더 합니다.  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>고가용성 재해 복구를 위한 SQLDriverConnect 지원  
 를 사용 하 여 `SQLDriverConnect` 클러스터에 연결 하는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 방법에 대 한 자세한 내용은 [고가용성, 재해 복구를 위한 SQL Server Native Client 지원](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)을 참조 하세요.  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>SPN(서비스 사용자 이름)에 대한 SQLDriverConnect 지원  
 SQLDDriverConnect는 프롬프트를 사용 하도록 설정 하면 ODBC 로그인 대화 상자를 사용 합니다. 이를 통해 주 서버 및 해당 장애 조치(Failover) 파트너 모두에 대한 SPN이 입력되도록 할 수 있습니다.  
  
 SQLDriverConnect는 새 연결 문자열 키워드 `ServerSPN` 및 `FailoverPartnerSPN`를 수락 하 고 SQL_COPT_SS_SERVER_SPN SQL_COPT_SS_FAILOVER_PARTNER_SPN 새 연결 특성을 인식 합니다.  
  
 연결 특성 값이 두 번 이상 지정된 경우 프로그래밍 방식으로 설정된 값이 DSN의 값 및 연결 문자열의 값보다 우선 순위가 높고 DSN의 값이 연결 문자열의 값보다 우선 순위가 높습니다.  
  
 연결이 열릴 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 및 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD를 연결을 여는 데 사용하는 인증 방법으로 설정합니다.  
  
 Spn에 대 한 자세한 내용은 [클라이언트 연결 &#40;ODBC&#41;에서 spn&#41; &#40;서비스 사용자 이름 ](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)을 참조 하세요.  
  
## <a name="examples"></a>예  
 다음 호출에서는에 `SQLDriverConnect`필요한 최소한의 데이터를 보여 줍니다.  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 다음 연결 문자열은 *Drivercompletion* 매개 변수 값이 SQL_DRIVER_NOPROMPT 경우 필요한 최소 데이터를 보여 줍니다.  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQLDriverConnect 함수](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 구현 세부 정보](odbc-api-implementation-details.md)   
 [Transact-sql&#41;&#40;ANSI_NULLS 설정](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [Transact-sql&#41;&#40;ANSI_PADDING 설정](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
