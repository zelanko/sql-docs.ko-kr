---
title: ODBC를 사용하여 연결
description: Microsoft ODBC Driver for SQL Server를 사용하여 Linux 또는 macOS에서 데이터베이스에 대한 연결을 만드는 방법에 대해 알아봅니다.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b99479883fd1cc74008d62a9c322226ed587244
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632813"
---
# <a name="connecting-to-sql-server"></a>SQL Server에 연결
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스와의 연결을 만들 수 있는 방법을 설명합니다.  
  
## <a name="connection-properties"></a>연결 속성  

Linux 및 macOS에서 지원되는 모든 연결 문자열 키워드 및 특성은 [DSN 및 연결 문자열 키워드 및 특성](../dsn-connection-string-attribute.md)을 참조하세요.

> [!IMPORTANT]  
> 데이터베이스 미러링(장애 조치(failover) 파트너 있음)을 사용하는 데이터베이스에 연결할 때 연결 문자열에 데이터베이스 이름을 지정하지 마세요. 대신, 쿼리를 실행하기 전에 **use** _database_name_ 명령을 보내 데이터베이스에 연결합니다.  
  
**Driver** 키워드에 전달된 값은 다음 중 하나일 수 있습니다.  
  
-   드라이버를 설치할 때 사용한 이름입니다.

-   드라이버를 설치하는 데 사용하는 템플릿 .ini 파일에 지정된 드라이버 라이브러리에 대한 경로입니다.  

DSN을 만들려면 현재 사용자만 액세스할 수 있는 사용자 DSN의 경우 **~/.odbc.ini** 파일(홈 디렉터리의`.odbc.ini`) 또는 시스템 DSN의 경우 `/etc/odbc.ini` 파일을 만들고(필요한 경우) 편집합니다(관리자 권한 필요). 다음은 DSN에 필요한 최소 항목을 표시하는 샘플 파일입니다.  

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

필요에 따라 서버에 연결할 프로토콜 및 포트를 지정할 수 있습니다. 예를 들어 **Server=tcp:** _servername_ **,12345**입니다. Linux 및 macOS 드라이버에서 지원되는 유일한 프로토콜은 `tcp`입니다.

고정 포트의 명명된 인스턴스에 연결하려면 <b>Server =</b>*servername*,**port_number**를 사용합니다. 버전 17.4 이전에서 동적 포트에 연결하는 것은 지원되지 않습니다.

또는 DSN 정보를 템플릿 파일에 추가하고 다음 명령을 실행하여 `~/.odbc.ini`에 추가할 수 있습니다.
 - **odbcinst -i -s -f** _template_file_  
 
`isql`을 사용하여 연결을 테스트해 드라이버가 작동하는지 확인할 수 있으며, 다음 명령을 사용할 수도 있습니다.
 - **bcp master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> -U <name> -P <password>**  

## <a name="using-tlsssl"></a>TLS/SSL 사용  
이전에 SSL(Secure Sockets Layer)로 알려진 TLS(전송 계층 보안)를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 연결을 암호화할 수 있습니다. TLS는 네트워크에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 사용자 이름과 암호를 보호합니다. 또한 TLS는 서버의 ID를 확인하여 MITM(메시지 가로채기) 공격으로부터 보호합니다.  

암호화를 사용하면 보안은 강화되지만 성능은 저하됩니다.

자세한 내용은 [SQL Server에 대한 연결 암호화](https://go.microsoft.com/fwlink/?LinkId=220900) 및 [유효성 검사 없이 암호화 사용](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)을 참조하세요.

**Encrypt** 및 **TrustServerCertificate**에 대한 설정과 관계없이 서버 로그인 자격 증명(사용자 이름 및 암호)은 상시 암호화됩니다. 다음 표는 **Encrypt** 및 **TrustServerCertificate** 를 설정할 때의 영향을 보여 줍니다.  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화되지 않습니다.|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화되지 않습니다.|  
|**Encrypt=yes**|서버 인증서를 확인합니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화됩니다.<br /><br />[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 인증서에 있는 주체 CN(일반 이름) 또는 SAN(주체 대체 이름)의 이름(또는 IP 주소)은 연결 문자열에 지정된 서버 이름(또는 IP 주소)과 정확하게 일치해야 합니다.|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화됩니다.|  

기본적으로 암호화된 연결에서 서버의 인증서를 항상 확인합니다. 그러나 자체 서명된 인증서가 있는 서버에 연결하는 경우에는 신뢰할 수 있는 인증 기관 목록에 대해 인증서 검사를 우회하는 `TrustServerCertificate` 옵션도 추가해야 합니다.  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
TLS는 OpenSSL 라이브러리를 사용합니다. 다음 표에서는 최소 지원되는 버전의 OpenSSL 및 각 플랫폼에 대한 기본 인증서 신뢰 저장소 위치를 보여 줍니다.

|플랫폼|최소 OpenSSL 버전|기본 인증서 신뢰 저장소 위치|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10.11, macOS 10.12, 10.13, 10.14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SUSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SUSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10, 19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04, 16.10, 17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

**SQLDriverConnect**를 사용하여 연결할 때 `Encrypt` 옵션을 사용하여 연결 문자열에서 암호화를 지정할 수도 있습니다.

## <a name="adjusting-the-tcp-keep-alive-settings"></a>TCP 연결 유지 설정 조정

ODBC 드라이버 17.4부터 드라이버가 연결 유지 패킷을 전송하고 응답을 수신하지 못할 경우 해당 패킷을 재전송하는 빈도를 구성할 수 있습니다.
구성하려면 `odbcinst.ini`의 드라이버 섹션 또는 `odbc.ini`의 DSN 섹션에 다음 설정을 추가합니다. DSN을 사용하여 연결하는 경우 드라이버는 DSN 섹션의 설정(있는 경우)을 사용합니다. 연결 문자열만 사용하여 연결하는 경우에는 `odbcinst.ini`의 드라이버 섹션에 있는 설정을 사용합니다. 어느 위치에도 설정이 없는 경우 드라이버는 기본값을 사용합니다.

- `KeepAlive=<integer>`는 연결을 유지하기 위해 TCP에서 연결 유지 패킷을 보내는 빈도를 제어합니다. 기본값은 **30**초입니다.

- `KeepAliveInterval=<integer>`은 응답이 수신될 때까지 연결 유지 재전송을 구분하는 간격을 결정합니다.  기본값은 **1** 초입니다.

## <a name="see-also"></a>참고 항목

- [Linux 기반 Microsoft ODBC Driver for SQL Server 설치](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [macOS 기반 Microsoft ODBC Driver for SQL Server 설치](install-microsoft-odbc-driver-sql-server-macos.md)
- [프로그래밍 지침](programming-guidelines.md)
