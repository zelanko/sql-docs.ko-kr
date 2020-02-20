---
title: 연결 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44843dedfe42374f832bb4ff03d819f5d08fbc7f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76916385"
---
# <a name="connection-options"></a>연결 옵션
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 결합형 배열에 허용되는 옵션(SQLSRV 드라이버에서 [sqlsrv_connect](../../connect/php/sqlsrv-connect.md)를 사용할 때) 또는 데이터 원본 이름(dsn)에 허용되는 키워드(PDO_SQLSRV 드라이버에서 [PDO::__construct](../../connect/php/pdo-construct.md)를 사용할 때)를 나열합니다.  

## <a name="table-of-connection-options"></a>연결 옵션 표

|키|값|Description|기본값|  
|-------|---------|---------------|-----------|  
|AccessToken|String|OAuth JSON 응답에서 추출된 Azure AD 액세스 토큰의 바이트 문자열입니다.<br /><br />연결 문자열에는 사용자 ID, 암호 또는 `Authentication` 키워드가 포함되지 않아야 합니다. 자세한 내용은 [Azure Active Directory 인증을 사용하여 연결](../../connect/php/azure-active-directory.md)을 참조하세요.|설정 안 됨.|
|APP|String|추적에서 사용되는 애플리케이션 이름을 지정합니다.|설정 안 됨.|  
|애플리케이션 의도|String|서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 가능한 값은 **ReadOnly** 및 **ReadWrite**입니다.<br /><br />[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대한 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 지원에 대한 자세한 내용은 [고가용성, 재해 복구 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|ReadWrite|
|AttachDBFileName|String|서버를 연결해야 하는 데이터베이스 파일을 지정합니다.|설정 안 됨.|
|인증|Key, Input, Predict, PredictOnly, None<br /><br />**SqlPassword**<br /><br />**ActiveDirectoryPassword**<br /><br />**ActiveDirectoryMsi**|인증 모드를 지정합니다.<br /><br />자세한 내용은 [Azure Active Directory 인증을 사용하여 연결](../../connect/php/azure-active-directory.md)을 참조하세요.|설정 안 됨.|
|CharacterSet<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|String|서버에 데이터를 보내는 데 사용되는 문자 집합을 지정합니다.<br /><br />가능한 값은 SQLSRV_ENC_CHAR 및 UTF-8입니다. 자세한 내용은 [방법: 기본 제공 UTF-8 지원을 사용하여 UTF-8 데이터 보내기 및 검색](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)을 참조하세요.|SQLSRV_ENC_CHAR|  
|ColumnEncryption|Key, Input, Predict, PredictOnly, None<br /><br />**Enabled**<br /><br />**사용 안 함**<br /><br />Enclave 증명을 위한 증명 프로토콜 및 URL을 식별하는 문자열입니다.|Always Encrypted 기능을 사용할 수 있는지 여부를 지정합니다. 증명 프로토콜 및 URL이 지정된 경우 [여기](../../connect/php/always-encrypted-secure-enclaves.md)에 설명된 대로 다른 요구 사항이 충족되면 보안 Enclave를 사용한 Always Encrypted가 사용하도록 설정됩니다.|사용 안 함|  
|ConnectionPooling|연결 풀링이 설정되면 1 또는 **true** 입니다.<br /><br />연결 풀링이 해제되면 0 또는 **false** 입니다.|연결이 연결 풀에서 할당되는지(1 또는 **true**) 할당되지 않는지(0 또는 **false**)를 지정합니다.<sup>1</sup>|**true**(1)|  
|ConnectRetryCount|0과 255(포함) 사이의 정수|포기하기 전에 끊어진 연결을 다시 설정하는 최대 시도 횟수입니다. 기본적으로 끊어진 연결을 다시 설정하기 위해 한 번 시도합니다. 값이 0이면 재연결을 시도하지 않습니다.|1|  
|ConnectRetryInterval|1과 60(포함) 사이의 정수|연결 다시 설정 시도 사이의 시간(초)입니다. 애플리케이션은 끊어진 연결을 검색하는 즉시 다시 연결을 시도하고 다시 시도하기 전에 `ConnectRetryInterval`초 동안 대기합니다. `ConnectRetryCount`가 0이면 이 키워드는 무시됩니다.|1|  
|데이터베이스|String|<sup>2</sup>을 설정할 연결에 대해 사용 중인 데이터베이스 이름을 지정합니다.|사용할 로그인에 대한 기본 데이터베이스입니다.|  
|DecimalPlaces<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|0과 4(포함) 사이의 정수|가져온 money 값의 서식을 지정할 때 소수 자릿수를 지정합니다.<br /><br />이 옵션은 `FormatDecimals`가 true인 경우에만 실행됩니다. 음의 정수 또는 4보다 큰 값은 무시됩니다.|기본 전체 자릿수 및 소수 자릿수|
|드라이버|String|SQL Server와 통신하는 데 사용되는 Microsoft ODBC 드라이버를 지정합니다.<br /><br />가능한 값은 다음과 같습니다.<br />ODBC Driver 17 for SQL Server<br />ODBC Driver 13 for SQL Server<br />ODBC Driver 11 for SQL Server(Windows만 해당)|Driver 키워드를 지정하지 않으면 Microsoft Drivers for PHP for SQL Server는 최신 버전의 ODBC부터 시작하여 시스템에서 지원되는 Microsoft ODBC 드라이버를 찾으려고 시도합니다.| 
|Encrypt|암호화가 설정되면 1 또는 **true** 입니다.<br /><br />암호화가 해제되면 0 또는 **false** 입니다.|SQL Server와의 통신이 암호화되었는지(1 또는 **true**) 또는 암호화되지 않았는지(0 또는 **false**)<sup>3</sup> 여부를 지정합니다.|**false**(0)|  
|Failover_Partner|String|주 서버를 사용할 수 없을 때 사용할 데이터베이스 미러의 인스턴스 및 서버(사용하도록 설정되고 구성된 경우)를 지정합니다.<br /><br />`MultiSubnetFailover`에서 `Failover_Partner`를 사용하는 데 제한 사항이 있습니다. 자세한 내용은 [고가용성, 재해 복구를 위한 JDBC 드라이브 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.<br /><br />ODBC 드라이버가 Linux 또는 macOS에서 데이터베이스 미러링을 지원하지 않으므로 Linux 또는macOS에서는 이 옵션이 지원되지 않습니다. 대신 Always On 가용성 그룹을 사용하여 `MultiSubnetFailover` 및 `TransparentNetworkIPResolution` 옵션을 설정합니다.|설정 안 됨.|
|FormatDecimals<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|1 또는 **true** 페치되는 10진수 문자열의 형식을 지정합니다.<br /><br />0 또는 **false** 기본 10진수 서식 지정 동작입니다.|해당하는 경우 10진수 문자열에 앞에 오는 0을 추가할지 여부를 지정하고 money 형식의 서식을 지정하기 위한 `DecimalPlaces` 옵션을 사용하도록 설정합니다. false로 유지하면, 1 미만의 값에서 앞에 오는 0을 생략하고 정확한 전체 자릿수를 반환하는 기본 동작이 사용됩니다.<br /><br />자세한 내용은 [Formatting Decimal Strings and Money Values](../../connect/php/formatting-decimals-sqlsrv-driver.md)(10진수 문자열 및 Money 값 서식 지정)를 참조하세요.|**false**(0)|
|KeyStoreAuthentication|**KeyVaultPassword**<br /><br />**KeyVaultClientSecret**|Azure Key Vault에 액세스하기 위한 인증 방법입니다. `KeyStorePrincipalId` 및 `KeyStoreSecret`에 사용되는 자격 증명의 유형을 제어합니다. 자세한 내용은 [Azure Key Vault 사용](../../connect/php/using-always-encrypted-php-drivers.md#using-azure-key-vault)을 참조하세요.|설정 안 됨.|
|KeyStorePrincipalId|String|Azure Key Vault에 액세스하려는 계정에 대한 식별자입니다. <br /><br />`KeyStoreAuthentication`이 **KeyVaultPassword**인 경우 Azure Active Directory 사용자 이름이어야 합니다. <br /><br />`KeyStoreAuthentication`이 **KeyVaultClientSecret**인 경우 애플리케이션 클라이언트 ID여야 합니다.|설정 안 됨.|
|KeyStoreSecret|String|Azure Key Vault에 액세스하려는 계정에 대한 자격 증명 비밀입니다. <br /><br />`KeyStoreAuthentication`이 **KeyVaultPassword**인 경우 Azure Active Directory 암호여야 합니다. <br /><br />`KeyStoreAuthentication`이 **KeyVaultClientSecret**인 경우 애플리케이션 클라이언트 비밀이어야 합니다.|설정 안 됨.|
|언어|String|서버가 반환하는 메시지의 언어를 지정합니다. 사용 가능한 언어는 `sys.syslanguages` 표에 나와 있습니다. <br /><br />이 옵션은 현재는 메시지가 영어로만 제공되므로 드라이버 자체에서 사용되는 언어에 영향을 주지 않으며, 클라이언트 시스템에 설치된 지역화 버전에 따라 언어가 결정되는 기본 ODBC 드라이버의 언어에 영향을 주지 않습니다. 따라서 이 설정을 변경하면 메시지가 PHP 드라이버, ODBC 드라이버 또는 SQL Server에서 나왔는지에 따라 다른 언어로 반환될 수 있습니다.|기본값은 SQL Server에서 설정된 언어입니다.|
|LoginTimeout|정수(SQLSRV 드라이버)<br /><br />문자열(PDO_SQLSRV 드라이버)|연결 시도가 실패할 때까지 기다리는 시간(초)을 지정합니다.|시간 제한이 없습니다.|  
|MultipleActiveResultSets|MARS(Multiple Active Result Set)를 사용하려면 1 또는 **true** 입니다.<br /><br />MARS(Multiple Active Result Set)를 사용하지 않으려면 0 또는 **false** 입니다.|MARS(Multiple Active Result Set)에 대한 지원을 사용하지 않도록 설정하거나 명시적으로 사용하도록 설정합니다.<br /><br />자세한 내용은 [방법: MARS&#40;MARS(Multiple Active Result Set)&#41;를 사용하지 않도록 설정](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)을 참조하세요.|true(1)|  
|MultiSubnetFailover|String|`multiSubnetFailover=yes` 가용성 그룹 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]를 지정하십시오. `multiSubnetFailover=yes`는 현재 활성 상태인 서버를 더 빠르게 검색하고 연결할 수 있도록 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 구성합니다. 가능한 값은 예 및 아니요입니다.<br /><br />[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대한 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 지원에 대한 자세한 내용은 [고가용성, 재해 복구 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|예|  
|PWD<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|String|SQL Server 인증<sup>4</sup>에 연결될 때 사용할 사용자 ID와 연결된 암호를 지정합니다.|설정 안 됨.|  
|QuotedId|SQL-92 규칙을 사용하려면 1 또는 **true**입니다.<br /><br />레거시 규칙을 사용하려면 0 또는 **false** 입니다.|따옴표로 묶은 식별자에 대해 SQL-92 규칙을 사용할지(1 또는 **true**) 레거시 Transact-SQL 규칙을 사용할지(0 또는 **false**) 여부를 지정합니다.|**true**(1)|  
|ReturnDatesAsStrings<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|날짜 및 시간 형식을 문자열로 반환하려면 1 또는 **true** 입니다.<br /><br />날짜 및 시간 형식을 PHP **DateTime** 형식으로 반환하려면 0 또는 **false** 입니다.|날짜 및 시간 형식(datetime, smalldatetime, date, time, datetime2, datetimeoffset)을 문자열 또는 PHP 형식으로 검색합니다. 자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 문자열로 검색](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)을 참조하세요. <br /><br />PDO_SQLSRV 드라이버를 사용하는 경우 별도로 지정하지 않는 한 날짜가 문자열로 반환됩니다. 자세한 내용은 [방법: PDO_SQLSRV 드라이버를 사용하여 날짜 및 시간 형식을 PHP DateTime 개체로 검색](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)을 참조하세요.|**false**|
|스크롤 가능|String|"버퍼됨"은 클라이언트 쪽(버퍼됨) 커서를 원한다는 것을 나타내며 메모리에서 전체 결과 집합을 캐시할 수 있습니다. 자세한 내용은 [커서 유형&#40;SQLSRV 드라이버&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)를 참조하세요.|정방향 전용 커서|  
|서버<br /><br />(SQLSRV 드라이버에서 지원되지 않음)|String|연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스입니다.<br /><br />또한 AlwaysOn 가용성 그룹에 연결하기 위해 가상 네트워크 이름을 지정할 수 있습니다. [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]에 대한 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 지원에 대한 자세한 내용은 [고가용성, 재해 복구 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.|서버는 필수 키워드입니다(연결 문자열에서 첫 번째 키워드가 될 필요는 없음). 서버 이름이 키워드에 전달되지 않은 경우 로컬 인스턴스에 연결하기 위해 시도합니다.<br /><br />서버에 전달된 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름 또는 인스턴스의 IP 주소일 수 있습니다. 필요에 따라 포트 번호를 지정할 수 있습니다(예: `sqlsrv:server=(local),1033`).<br /><br />[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 의 버전 3.0부터는 `server=(localdb)\instancename`을 사용하여 LocalDB 인스턴스를 지정할 수도 있습니다. 자세한 내용은 [LocalDB 지원](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)을 참조하세요.|  
|TraceFile|String|추적 데이터에 사용되는 파일에 대한 경로를 지정합니다.|설정 안 됨.|  
|TraceOn|추적을 사용하도록 설정하려면 1 또는 **true** 입니다.<br /><br />추적을 사용하지 않도록 설정하려면 0 또는 **false** 입니다.|설정되는 연결에 대해 ODBC 추적이 사용하도록 설정되는지(1 또는 **true**) 사용하지 않도록 설정되는지(0 또는 **false**) 지정합니다.|**false**(0)|  
|TransactionIsolation|SQLSRV 드라이버는 다음 값을 사용합니다.<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />PDO_SQLSRV 드라이버는 다음 값을 사용 합니다.<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|트랜잭션 격리 수준을 지정합니다.<br /><br />트랜잭션 격리에 대한 자세한 내용은 SQL Server 설명서에서 [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)을 참조하세요.|SQLSRV_TXN_READ_COMMITTED<br /><br />또는<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|TransparentNetworkIPResolution|**사용** 또는 **사용 안 함**|호스트 이름의 첫 번째 확인된 IP가 응답하지 않고 호스트 이름과 연결된 여러 IP가 있는 경우 연결 시퀀스에 영향을 미칩니다.<br /><br />`MultiSubnetFailover`와 상호 작용하여 서로 다른 연결 시퀀스를 제공합니다. 자세한 내용은 [투명 네트워크 IP 확인](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) 또는 [투명 네트워크 IP 확인 사용](https://docs.microsoft.com/sql/connect/odbc/using-transparent-network-ip-resolution)을 참조하세요.|사용|
|TrustServerCertificate|인증서를 신뢰하려면 1 또는 **true** 입니다.<br /><br />인증서를 신뢰하지 않으려면 0 또는 **false** 입니다.|클라이언트가 자체 서명된 서버 인증서를 신뢰해야 하는지(1 또는 **true**) 또는 거부해야 하는지(0 또는 **false**) 여부를 지정합니다.|**false**(0)|  
|UID<br /><br />(PDO_SQLSRV 드라이버에서 지원되지 않음)|String|SQL Server 인증<sup>4</sup>과 연결할 때 사용할 사용자 ID를 지정합니다.|설정 안 됨.|  
|WSID|String|추적용 컴퓨터의 이름을 지정합니다.|설정 안 됨.|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. `ConnectionPooling` 특성을 사용하여 Linux 및 Mac에서 연결 풀링을 사용하거나 사용하지 않도록 설정할 수 없습니다. [연결 풀링(Microsoft Drivers for PHP for SQL Server)](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)을 참조하세요.

2. 설정된 연결에서 실행되는 모든 쿼리는 `Database` 특성에서 지정하는 데이터베이스에 대해 만들어집니다. 그러나 사용자에게 적절한 권한이 있는 경우 정규화된 이름을 사용하여 다른 데이터베이스의 데이터에 액세스할 수 있습니다. 예를 들어 *마스터* 데이터베이스가 `Database` 연결 특성으로 설정된 경우 정규화된 이름을 사용하여 *AdventureWorks.HumanResources.Employee* 테이블에 액세스하는 Transact-SQL 쿼리를 계속 실행할 수 있습니다.  

3. `Encryption`을 사용하도록 설정하면 데이터를 암호화하는 데 필요한 계산 오버헤드로 인해 일부 애플리케이션의 성능에 영향을 줄 수 있습니다.  

4. `UID` 및 `PWD` 특성은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증과 연결될 때 둘 다 설정되어야 합니다.  

지원되는 많은 키가 ODBC 연결 문자열 특성입니다. ODBC 연결 문자열에 대한 정보는 [SQL Native Client에서 연결 문자열 키워드 사용](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하세요.

## <a name="see-also"></a>참고 항목  
[서버에 연결](../../connect/php/connecting-to-the-server.md)  
