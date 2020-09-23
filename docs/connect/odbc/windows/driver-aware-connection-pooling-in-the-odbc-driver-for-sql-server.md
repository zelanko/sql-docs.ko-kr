---
title: ODBC 드라이버에서 드라이버 인식 연결 풀링
description: Windows 기반의 Microsoft ODBC Driver for SQL Server에서 드라이버 인식 연결 풀링 개선 사항을 알아봅니다.
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1d8700e6868781480771c4a62f2a5fc6c92ddfc
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288115"
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>ODBC Driver for SQL Server에서 드라이버 인식 연결 풀링
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 지원합니다. 이 항목은 Windows 기반의 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 드라이버 인식 연결 풀링 개선 사항을 설명합니다.  
  
-   연결 속성에 관계없이 `SQLDriverConnect`를 사용하는 연결은 `SQLConnect`를 사용하는 연결과는 별도의 풀로 이동합니다.
- [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 및 드라이버 인식 연결 풀링을 사용하는 경우 드라이버가 풀에서 연결을 분리하기 위해 현재 스레드에 대한 Windows 사용자의 보안 컨텍스트를 사용하지 않습니다. 즉, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하는 Windows 가장 시나리오에 대해 연결이 동일한 매개 변수를 사용하고 동일한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증 자격 증명을 사용하여 백 엔드에 연결하는 경우 여러 Windows 사용자가 잠재적으로 동일한 연결 풀을 사용할 수 있다는 것입니다. Windows 인증 및 드라이버 인식 연결 풀링을 사용하는 경우 드라이버가 풀에서 연결을 분리하기 위해 현재 Windows 사용자의 보안 컨텍스트를 사용합니다. 즉, Windows의 가장 시나리오에 대해 연결이 동일한 매개 변수를 사용하는 경우에도 여러 Windows 사용자가 연결을 공유하지 않습니다.
- Azure Active Directory 및 드라이버 인식 연결 풀링을 사용하는 경우 드라이버는 인증 값을 사용하여 연결 풀의 멤버 자격을 확인합니다.
  
-   드라이버 인식 연결 풀링에서 잘못된 연결이 풀에서 반환되지 않도록 방지합니다.  
  
-   드라이버 인식 연결 풀링이 드라이버별 연결 특성을 인식합니다. 따라서 연결에서 읽기 전용으로 설정된 `SQL_COPT_SS_APPLICATION_INTENT`를 사용하는 경우 해당 연결은 자체 연결 풀을 가져옵니다.
-   `SQL_COPT_SS_ACCESS_TOKEN` 특성을 설정하면 연결이 별도로 풀링됩니다. 
  
연결 문자열과 풀링된 연결 문자열 사이에서 다음 연결 특성 ID 또는 연결 문자열 키워드 중 하나가 다른 경우 드라이버가 풀링된 연결을 사용합니다. 그러나 모든 연결 특성 ID 또는 연결 문자열 키워드가 일치하면 성능이 향상됩니다. 풀에서 연결을 일치시키기 위해 드라이버가 특성을 재설정합니다. 다음 매개 변수를 재설정하려면 추가 네트워크 호출이 필요하기 때문에 성능이 저하됩니다.  
  
-    다음 연결 특성 또는 연결 키워드 중 두 개 이상이 다르면 풀링된 연결이 사용되지 않습니다.  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   다음 연결 키워드에서 연결 문자열과 풀링된 연결 문자열 사이에 차이가 있는 경우 풀링된 연결이 사용되지 않습니다.  
  
    |키워드|ODBC 드라이버 17/13|ODBC 드라이버 11|
    |-|-|-|
    |`Address`|예|예|
    |`AnsiNPW`|예|예|
    |`App`|예|예|
    |`ApplicationIntent`|예|예|  
    |`Authentication`|예|예|
    |`ColumnEncryption`|예|예|
    |`Database`|예|예|
    |`Encrypt`|예|예|  
    |`Failover_Partner`|예|예|
    |`FailoverPartnerSPN`|예|예|
    |`MARS_Connection`|예|예|
    |`Network`|예|예|
    |`PWD`|예|예|
    |`Server`|예|예|
    |`ServerSPN`|예|예|
    |`TransparentNetworkIPResolution`|예|예|
    |`Trusted_Connection`|예|예|
    |`TrustServerCertificate`|예|예|
    |`UID`|예|예|
    |`WSID`|예|예|
    
- 다음 연결 특성에서 연결 문자열과 풀링된 연결 문자열 사이에 차이가 있는 경우 풀링된 연결이 사용되지 않습니다.  
  
    |attribute|ODBC 드라이버 17/13|ODBC 드라이버 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|예|예|
    |`SQL_ATTR_PACKET_SIZE`|예|예|
    |`SQL_COPT_SS_ANSI_NPW`|예|예|
    |`SQL_COPT_SS_ACCESS_TOKEN`|예|예|
    |`SQL_COPT_SS_AUTHENTICATION`|예|예|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|예|예|
    |`SQL_COPT_SS_BCP`|예|예|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|예|예|
    |`SQL_COPT_SS_CONCAT_NULL`|예|예|
    |`SQL_COPT_SS_ENCRYPT`|예|예|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|예|예|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|예|예|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|예|예|
    |`SQL_COPT_SS_MARS_ENABLED`|예|예|
    |`SQL_COPT_SS_OLDPWD`|예|예|
    |`SQL_COPT_SS_SERVER_SPN`|예|예|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|예|예|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|예|예|
    |`SQL_COPT_SS_TNIR`|예|예|
 
-   추가 네트워크를 호출하지 않고 드라이버가 다음 연결 키워드 및 특성을 재설정하고 조정할 수 있습니다. 드라이버는 연결에 잘못된 정보가 포함되지 않도록 이러한 매개 변수를 다시 설정합니다.  
  
     드라이버 관리자가 연결을 풀의 연결과 일치시키려고 할 때 이러한 연결 키워드는 고려되지 않습니다. (이러한 매개 변수 중 하나를 변경하는 경우에도 기존 연결을 재사용할 수 있습니다. 드라이버가 필요에 따라 옵션을 재설정합니다. 이러한 특성은 추가로 네트워크를 호출하지 않고 클라이언트 쪽에서 재설정할 수 있습니다.  
  
    |키워드|ODBC 드라이버 17/13|ODBC 드라이버 11|  
    |-|-|-|  
    |`AutoTranslate`|예|예|
    |`Description`|예|예|
    |`MultisubnetFailover`|예|예|  
    |`QueryLog_On`|예|예|
    |`QueryLogFile`|예|예|
    |`QueryLogTime`|예|예|
    |`Regional`|예|예|
    |`StatsLog_On`|예|예|
    |`StatsLogFile`|  예|예|
  
     다음 연결 특성 중 하나를 변경하는 경우 기존 연결을 재사용할 수 있습니다.  필요에 따라 드라이버가 값을 재설정합니다. 드라이버가 추가로 네트워크를 호출하지 않고 클라이언트에서 이러한 특성을 재설정할 수 있습니다.  
  
    |attribute|ODBC 드라이버 17/13|ODBC 드라이버 11|  
    |-|-|-|  
    |모든 문 특성|예|예|
    |`SQL_ATTR_AUTOCOMMIT`|예|예|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  예|예|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|예|예|
    |`SQL_ATTR_LOGIN_TIMEOUT`|예|예|
    |`SQL_ATTR_ODBC_CURSORS`|  예|예|
    |`SQL_COPT_SS_PERF_DATA`|예|예|
    |`SQL_COPT_SS_PERF_DATA_LOG`|예|예|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| 예|예| 
    |`SQL_COPT_SS_PERF_QUERY`|예|예|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|예|예|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  예|예|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|예|예|
    |`SQL_COPT_SS_TRANSLATE`|예|예|
    |`SQL_COPT_SS_USER_DATA`|  예|예|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|예|예|  
  
## <a name="see-also"></a>참고 항목  
 [Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
