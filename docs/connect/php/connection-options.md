---
title: "연결 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
caps.latest.revision: "37"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4fcec3597676efa5feebc3fdb562a6dd19878278
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="connection-options"></a>연결 옵션
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 결합형 배열에 허용 되는 옵션 (사용 하는 경우 [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) SQLSRV 드라이버에서) 또는 데이터 원본 이름 (dsn)에 허용 되는 키워드 (사용 하는 경우 [:: __construct ](../../connect/php/pdo-construct.md) PDO_SQLSRV 드라이버에서).  

|Key|값|설명|기본값|  
|-------|---------|---------------|-----------|  
|APP|문자열|추적에서 사용되는 응용 프로그램 이름을 지정합니다.|설정된 값이 없습니다.|  
|응용 프로그램 의도|문자열|서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 가능한 값은 ReadOnly 및 ReadWrite입니다.<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 사용에 필요한 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]지원에 대한 자세한 내용은 [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(PHP Driver for SQL Server의 고가용성, 재해 복구 지원)를 참조하세요.|ReadWrite|  
|AttachDBFileName|문자열|서버를 연결해야 하는 데이터베이스 파일을 지정합니다.|설정된 값이 없습니다.|  
|인증|Key, Input, Predict, PredictOnly, None<br /><br />' SqlPassword'<br /><br />' ActiveDirectoryPassword'|인증 모드를 지정 합니다.|설정 되지 않았습니다.|  
|CharacterSet<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|문자열|서버에 데이터를 보내는 데 사용되는 문자 집합을 지정합니다.<br /><br />가능한 값은 SQLSRV_ENC_CHAR 및 UTF-8입니다. 자세한 내용은 [How to: Send and Retrieve UTF-8 Data Using Built-In UTF-8 Support](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)을 참조하세요.|SQLSRV_ENC_CHAR|  
|ConnectionPooling|연결 풀링이 설정되면 1 또는 **true** 입니다.<br /><br />연결 풀링이 해제되면 0 또는 **false** 입니다.|연결이 연결 풀에서 할당 되었는지 여부를 지정 합니다 (1 또는 **true**) 아닌지 (0 또는 **false**).<sup> 1</sup>|**true 이면** (1)|  
|데이터베이스|문자열|설정 되는 연결에 대 한 사용 데이터베이스의 이름을 지정<sup>2</sup>합니다.|사용할 로그인에 대한 기본 데이터베이스입니다.|  
|Encrypt|암호화가 설정되면 1 또는 **true** 입니다.<br /><br />암호화가 해제되면 0 또는 **false** 입니다.|SQL Server와의 통신이 암호화 되는지 여부를 지정 합니다 (1 또는 **true**) 또는 암호화 되지 않았는지 (0 또는 **false**)<sup>3</sup>합니다.|**false** (0)|  
|Failover_Partner|문자열|주 서버를 사용할 수 없을 때 사용할 데이터베이스 미러의 인스턴스 및 서버(사용하도록 설정되고 구성된 경우)를 지정합니다.<br /><br />MultiSubnetFailover에서 Failover_Partner 사용에 대한 제한이 있습니다. 자세한 내용은 [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(PHP Driver for SQL Server의 고가용성, 재해 복구 지원)를 참조하세요.|설정된 값이 없습니다.|  
|LoginTimeout|정수(SQLSRV 드라이버)<br /><br />문자열(PDO_SQLSRV 드라이버)|연결 시도가 실패할 때까지 기다리는 시간(초)을 지정합니다.|시간 제한이 없습니다.|  
|MultipleActiveResultSets|MARS(Multiple Active Result Set)를 사용하려면 1 또는 **true** 입니다.<br /><br />MARS(Multiple Active Result Set)를 사용하지 않으려면 0 또는 **false** 입니다.|MARS(Multiple Active Result Set)에 대한 지원을 사용하지 않도록 설정하거나 명시적으로 사용하도록 설정합니다.<br /><br />자세한 내용은 참조 [하는 방법: Multiple Active Resultsets 사용 안 함 &#40; MARS &#41; ](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md).|true(1)|  
|MultiSubnetFailover|문자열|항상 지정 **multiSubnetFailover = yes** 의 가용성 그룹 수신기에 연결할 때는 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 가용성 그룹 또는 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 장애 조치 클러스터 인스턴스의 합니다. **multiSubnetFailover = yes** 구성 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 더 빠른 감지와 (현재) 활성 서버 연결을 제공 하도록 합니다. 가능한 값은 예 및 아니요입니다.<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 사용에 필요한 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]지원에 대한 자세한 내용은 [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(PHP Driver for SQL Server의 고가용성, 재해 복구 지원)를 참조하세요.|아니요|  
|PWD<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|문자열|SQL Server 인증으로 연결할 때 사용할 사용자 ID와 연결 된 암호를 지정<sup>4</sup>합니다.|설정된 값이 없습니다.|  
|QuotedId|1 또는 **true** sql-92 규칙을 사용 하도록 합니다.<br /><br />레거시 규칙을 사용하려면 0 또는 **false** 입니다.|따옴표 붙은 식별자에 대 한 sql-92 규칙을 사용할지 여부를 지정 (1 또는 **true**) 레거시 TRANSACT-SQL 규칙을 사용 하거나 (0 또는 **false**).|**true 이면** (1)|  
|ReturnDatesAsStrings<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|날짜 및 시간 형식을 문자열로 반환하려면 1 또는 **true** 입니다.<br /><br />날짜 및 시간 형식을 PHP **DateTime** 형식으로 반환하려면 0 또는 **false** 입니다.|날짜 및 시간 형식(datetime, date, time, datetime2 및 datetimeoffset)을 문자열 또는 PHP 형식으로 검색합니다. PDO_SQLSRV 드라이버를 사용하는 경우 날짜가 문자열로 반환됩니다. PDO_SQLSRV 드라이버에 **datetime** 유형입니다.<br /><br />자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)을 참조하세요.|**false**|  
|스크롤 가능|문자열|"버퍼됨"은 클라이언트 쪽(버퍼됨) 커서를 원한다는 것을 나타내며 메모리에서 전체 결과 집합을 캐시할 수 있습니다. 자세한 내용은 참조 [커서 유형 &#40; SQLSRV 드라이버 &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md).|정방향 전용 커서|  
|Server<br /><br />(SQLSRV 드라이버에서 지원되지 않음)|문자열|연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스입니다.<br /><br />또한 AlwaysOn 가용성 그룹에 연결하기 위해 가상 네트워크 이름을 지정할 수 있습니다. [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 사용에 필요한 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]지원에 대한 자세한 내용은 [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(PHP Driver for SQL Server의 고가용성, 재해 복구 지원)를 참조하세요.|서버는 필수 키워드입니다(연결 문자열에서 첫 번째 키워드가 될 필요는 없음). 서버 이름으로 키워드에 전달 되지 않으므로 로컬 인스턴스에 연결 하려면 시도가 이루어집니다.<br /><br />서버에 전달된 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스의 이름 또는 인스턴스의 IP 주소일 수 있습니다. 필요에 따라 포트 번호를 지정할 수 있습니다 (예를 들어 `sqlsrv:server=(local),1033`).<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 버전 3.0부터는 `server=(localdb)\instancename`을 사용하여 LocalDB 인스턴스를 지정할 수도 있습니다. 자세한 내용은 [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)을 참조하세요.|  
|TraceFile|문자열|추적 데이터에 사용되는 파일에 대한 경로를 지정합니다.|설정된 값이 없습니다.|  
|TraceOn|추적을 사용하도록 설정하려면 1 또는 **true** 입니다.<br /><br />추적을 사용하지 않도록 설정하려면 0 또는 **false** 입니다.|ODBC 추적이 사용 되는지 여부를 지정 합니다 (1 또는 **true**) 또는 해제 (0 또는 **false**) 설정 되는 연결에 대 한 합니다.|**false** (0)|  
|TransactionIsolation|SQLSRV 드라이버는 다음 값을 사용합니다.<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />PDO_SQLSRV 드라이버는 다음 값을 사용 합니다.<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|트랜잭션 격리 수준을 지정합니다.<br /><br />트랜잭션 격리에 대한 자세한 내용은 SQL Server 설명서에서 [SET TRANSACTION ISOLATION LEVEL](http://go.microsoft.com/fwlink/?LinkID=191497) 을 참조하세요.|SQLSRV_TXN_READ_COMMITTED<br /><br />또는<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|TransparentNetworkIPResolution|**활성화** 또는 **사용 안 함**|호스트 이름을와 관련 된 첫 번째 해결 호스트의 IP가 응답 하지 않으면 되며 여러 Ip 연결 시퀀스를에 영향을 줍니다.<br /><br />다른 연결 시퀀스를 제공 하는 MultiSubnetFailover와 상호 작용 합니다. 자세한 내용은 참조 [투명 네트워크 IP 확인 사용 하 여](https://docs.microsoft.com/en-us/sql/connect/odbc/using-transparent-network-ip-resolution)합니다.|설정|
|TrustServerCertificate|인증서를 신뢰하려면 1 또는 **true** 입니다.<br /><br />인증서를 신뢰하지 않으려면 0 또는 **false** 입니다.|클라이언트 신뢰 해야 하는지 여부를 지정 합니다 (1 또는 **true**) 하거나 거부 (0 또는 **false**) 자체 서명한 서버 인증서.|**false** (0)|  
|UID<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|문자열|SQL Server 인증으로 연결 될 때 사용할 사용자 ID를 지정<sup>4</sup>합니다.|설정된 값이 없습니다.|  
|WSID|문자열|추적용 컴퓨터의 이름을 지정합니다.|설정된 값이 없습니다.|  

1. `ConnectionPooling` 특성을 설정/해제 Linux와 Mac.에서 연결 풀링을 사용할 수 없습니다 참조 [연결 풀링 (Microsoft Drivers for PHP for SQL Server)](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)합니다.

2. 지정 된 데이터베이스에 설정된 된 연결에서 실행 되는 모든 쿼리 적용는 *데이터베이스* 특성입니다. 그러나 사용자에 적절 한 권한이 있으면 다른 데이터베이스의에서 데이터 정규화 된 이름을 사용 하 여 액세스할 수 있습니다. 예를 들어 경우는 *마스터* 으로 설정 된 데이터베이스는 *데이터베이스* 계속 액세스 하는 Transact SQL 쿼리를 실행할 수는 연결 특성은  *AdventureWorks.HumanResources.Employee* 정규화 된 이름을 사용 하 여 테이블입니다.  

3. *암호화* 를 사용하도록 설정하면 데이터를 암호화하는 데 필요한 계산 오버헤드로 인해 일부 응용 프로그램의 성능에 영향을 줄 수 있습니다.  

4. 연결할 *UID* 와 *PWD* 특성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증과 연결될 때 둘 다 설정되어야 합니다.  

지원되는 많은 키가 ODBC 연결 문자열 특성입니다. ODBC 연결 문자열에 대한 정보는 [SQL Native Client에서 연결 문자열 키워드 사용](http://go.microsoft.com/fwlink/?LinkId=105504)을 참조하세요.  

## <a name="see-also"></a>참고 항목  
[서버에 연결](../../connect/php/connecting-to-the-server.md)  
