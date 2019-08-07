---
title: SQL Server에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 486d26dd3afeb91cb43181875e22592fb482af5f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702800"
---
# <a name="connecting-to-sql-server"></a>SQL Server에 연결
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스와의 연결을 만들 수 있는 방법을 설명합니다.  
  
## <a name="connection-properties"></a>연결 속성  

Linux 및 Mac에서 지원 되는 모든 연결 문자열 키워드 및 특성의 [DSN 및 연결 문자열 키워드 및 특성](../../../connect/odbc/dsn-connection-string-attribute.md) 을 참조 하세요.

> [!IMPORTANT]  
> 데이터베이스 미러링(장애 조치(failover) 파트너 있음)을 사용하는 데이터베이스에 연결할 때 연결 문자열에 데이터베이스 이름을 지정하지 마세요. 대신 쿼리를 실행하기 전에 **use** _database_name_ 명령을 보내 데이터베이스에 연결합니다.  
  
**Driver** 키워드에 전달 된 값은 다음 중 하나일 수 있습니다.  
  
-   드라이버를 설치할 때 사용한 이름입니다.

-   드라이버를 설치하는 데 사용하는 템플릿 .ini 파일에 지정된 드라이버 라이브러리에 대한 경로입니다.  

DSN을 만들려면 (필요한 경우) 파일을 만들고 (홈 디렉터리에서) **/.odbc.ini** (`.odbc.ini` 홈 디렉터리의) 파일을 편집 하 여 현재 사용자 또는 `/etc/odbc.ini` 시스템 dsn (관리 권한 필요)에만 액세스할 수 있도록 합니다. 다음은 DSN에 필요한 항목을 표시하는 샘플 파일입니다.  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

필요에 따라 서버에 연결할 프로토콜 및 포트를 지정할 수 있습니다. 예를 들어 **Server = tcp:** _servername_ **, 12345**입니다. Linux 및 macOS 드라이버에서 지원 되는 유일한 프로토콜은 `tcp`입니다.

고정 포트의 명명된 인스턴스에 연결하려면 <b>Server =</b>*servername*,**port_number**를 사용합니다. 버전 17.4 이전에서 동적 포트에 연결하는 것은 지원되지 않습니다.

또는 DSN 정보를 템플릿 파일에 추가하고 다음 명령을 실행하여 `~/.odbc.ini`에 추가할 수 있습니다.
 - **odbcinst -i -s -f** _template_file_  
 
를 사용 `isql` 하 여 연결을 테스트 하 여 드라이버가 작동 하는지 확인 하거나 다음 명령을 사용할 수 있습니다.
 - **bcp INFORMATION_SCHEMA out ...s <server> -U <name> -P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>SSL(Secure Sockets Layer) 사용  
SSL(Secure Sockets Layer)을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 연결을 암호화할 수 있습니다. SSL은 네트워크에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름 및 암호를 보호합니다. SSL은 또한 MITM(메시지 가로채기) 공격으로부터 보호하기 위해 서버의 ID를 확인합니다.  

암호화를 사용하면 보안은 강화되지만 성능은 저하됩니다.

자세한 내용은 [SQL Server에 대 한 연결 암호화](https://go.microsoft.com/fwlink/?LinkId=220900) 및 [유효성 검사 없이 암호화 사용](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)을 참조 하세요.

**Encrypt** 및 **TrustServerCertificate**에 대한 설정과 관계없이 서버 로그인 자격 증명(사용자 이름 및 암호)은 상시 암호화됩니다. 다음 표는 **Encrypt** 및 **TrustServerCertificate** 를 설정할 때의 영향을 보여 줍니다.  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화되지 않습니다.|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화되지 않습니다.|  
|**Encrypt=yes**|서버 인증서를 확인합니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화됩니다.<br /><br />[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 인증서에 있는 주체 CN(일반 이름) 또는 SAN(주체 대체 이름)의 이름(또는 IP 주소)은 연결 문자열에 지정된 서버 이름(또는 IP 주소)과 정확하게 일치해야 합니다.|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화됩니다.|  

기본적으로 암호화된 연결에서 서버의 인증서를 항상 확인합니다. 그러나 자체 서명 된 인증서가 있는 서버에 연결 하는 경우에는 신뢰할 수 있는 인증 `TrustServerCertificate` 기관 목록에 대해 인증서 검사를 무시 하는 옵션도 추가 해야 합니다.  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL은 OpenSSL 라이브러리를 사용합니다. 다음 표에서는 최소 지원되는 버전의 OpenSSL 및 각 플랫폼에 대한 기본 인증서 신뢰 저장소 위치를 보여 줍니다.

|플랫폼|최소 OpenSSL 버전|기본 인증서 신뢰 저장소 위치|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10.11, macOS 10.12, 10.13, 10.14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SuSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10, 19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04, 16.10, 17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

**SQLDriverConnect**를 사용 하 여 연결 하는 경우 옵션을 `Encrypt` 사용 하 여 연결 문자열에 암호화를 지정할 수도 있습니다.

## <a name="adjusting-the-tcp-keep-alive-settings"></a>TCP keep-alive 설정 조정

ODBC 드라이버 17.4부터 드라이버가 수신 되지 않는 패킷을 전송 하 고 응답을 수신 하지 않을 때 해당 패킷을 재전송 하는 빈도는 구성 가능 합니다.
을 구성 하려면의 드라이버 섹션 `odbcinst.ini`또는의 `odbc.ini`DSN 섹션에 다음 설정을 추가 합니다. DSN을 사용 하 여 연결 하는 경우 드라이버는 DSN 섹션 (있는 경우)의 설정을 사용 합니다. 그렇지 않고 연결 문자열만 사용 하 여 연결 하는 경우에는의 `odbcinst.ini`드라이버 섹션에 있는 설정을 사용 합니다. 어느 위치에도 설정이 없는 경우 드라이버는 기본값을 사용 합니다.

- `KeepAlive=<integer>`TCP에서 연결 유지 패킷을 전송 하 여 유휴 연결이 그대로 유지 되는지 확인 하는 빈도를 제어 합니다. 기본값은 **30**초입니다.

- `KeepAliveInterval=<integer>`응답이 수신 될 때까지 keep-alive 재전송을 구분 하는 간격을 결정 합니다.  기본값은 **1** 초입니다.


## <a name="see-also"></a>참고 항목  
[Linux 및 macOS 기반 SQL Server용 Microsoft ODBC Driver 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)
