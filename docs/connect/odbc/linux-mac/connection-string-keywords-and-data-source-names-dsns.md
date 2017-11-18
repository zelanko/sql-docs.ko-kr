---
title: "연결 문자열 키워드 및 데이터 원본 이름 (Dsn) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508fcb62b7cf9ccd78c04b869add7acccb14f258
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="connection-string-keywords-and-data-source-names-dsns"></a>연결 문자열 키워드 및 DSN(데이터 원본 이름)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에 대 한 연결을 만들 수는 방법에 대해 설명 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
## <a name="connection-properties"></a>연결 속성  
이 버전의 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux 또는 macOS 다음 연결 키워드를 사용할 수 있습니다.  
  
||||||  
|-|-|-|-|-|  
|`Addr`|`Address`|`ApplicationIntent`|`AutoTranslate`|`Database`|
|`Driver`|`DSN`|`Encrypt`|`FileDSN`|`MARS_Connection`|  
|`MultiSubnetFailover`|`PWD`|`Server`|`Trusted_Connection`|`TrustServerCertificate`|  
|`UID`|`WSID`|`ColumnEncryption`|`TransparentNetworkIPResolution`||  

> [!IMPORTANT]  
> 데이터베이스 미러링(장애 조치(failover) 파트너 있음)을 사용하는 데이터베이스에 연결할 때 연결 문자열에 데이터베이스 이름을 지정하지 마세요. 대신 보내기는 **사용** *a s e _* 쿼리를 실행 하기 전에 데이터베이스에 연결 하는 명령입니다.  
  
이러한 키워드에 대한 자세한 내용은 [SQL Server Native Client에서 연결 문자열 키워드 사용](http://go.microsoft.com/fwlink/?LinkID=126696)의 ODBC 섹션을 참조하세요.  
  
에 전달 된 값은 **드라이버** 키워드는 다음 중 하나일 수 있습니다.  
  
-   드라이버를 설치할 때 사용한 이름입니다.

-   드라이버 라이브러리에 드라이버를 설치 하는 데 사용 하는 템플릿.ini 파일에 지정 된 경로입니다.  

DSN을 만들려면 (필요한 경우) 파일 만들기 및 편집는 **~/.odbc.ini** (`.odbc.ini` 홈 디렉터리에서)는 현재 사용자만 액세스할 수는 사용자 DSN에 대 한 또는 `/etc/odbc.ini` 시스템 dsn (관리자 권한이 필요 합니다.) 다음은 DSN에 대 한 최소 필요한 항목을 표시 하는 샘플 파일입니다.  

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

필요에 따라 서버에 연결할 프로토콜 및 포트를 지정할 수 있습니다. 예를 들어 **Server = tcp:***servername***, 12345**합니다. Linux와 macOS 드라이버에서 지 원하는 유일한 프로토콜은 `tcp`합니다.

명명 된 인스턴스에 정적 포트에 연결 하려면 <b>서버 =</b>*servername*,**port_number**합니다. 동적 포트에 연결 하는 것은 지원 되지 않습니다.  

템플릿 파일에 DSN 정보를 추가 하 고에 추가 하려면 다음 명령을 실행할 수 또는 `~/.odbc.ini` :
 - **odbcinst-i-f-s** *template_file*  
 
드라이버를 사용 하 여 작동 하는지 확인할 수 있습니다 `isql` 연결을 테스트 하려면이 명령을 사용 합니다.
 - **bcp master.INFORMATION_SCHEMA.TABLES 초과 outfile.dat 파일-S <server> -U <name> -P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>SSL(Secure Sockets Layer) 사용  
Secure Sockets Layer (SSL)를 사용 하 여 연결을 암호화 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. SSL 보호 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 사용자 이름 및 네트워크를 통해 암호입니다. SSL은 또한 MITM(메시지 가로채기) 공격으로부터 보호하기 위해 서버의 ID를 확인합니다.  

암호화를 사용하면 보안은 강화되지만 성능은 저하됩니다.

자세한 내용은 참조 [SQL Server 연결 암호화](http://go.microsoft.com/fwlink/?LinkId=220900) 및 [유효성 검사 없이 암호화를 사용 하 여](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)합니다.

**Encrypt** 및 **TrustServerCertificate**에 대한 설정과 관계없이 서버 로그인 자격 증명(사용자 이름 및 암호)은 상시 암호화됩니다. 다음 표는 **Encrypt** 및 **TrustServerCertificate** 를 설정할 때의 영향을 보여 줍니다.  

||**TrustServerCertificate = 아니요**|**TrustServerCertificate = yes**|  
|-|-------------------------------------|------------------------------------|  
|**암호화 = 아니요**|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화되지 않습니다.|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화되지 않습니다.|  
|**암호화 = 예**|서버 인증서를 확인합니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화됩니다.<br /><br />주체 CN (일반 이름) 또는 SAN 주체 대체 이름 ()의 이름 (또는 IP 주소)는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 인증서는 연결 문자열에 지정 된 서버 이름 (또는 IP 주소)에 정확히 일치 해야 합니다.|서버 인증서를 확인하지 않습니다.<br /><br />클라이언트와 서버 간에 전송되는 데이터가 암호화됩니다.|  

기본적으로 암호화된 연결에서 서버의 인증서를 항상 확인합니다. 그러나 자체 서명 된 인증서가 있는 서버에 연결 하는 경우 추가적으로 `TrustServerCertificate` 신뢰할 수 있는 인증 기관의 목록 비교 하 여 인증서 검사를 무시 하는 옵션:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL은 OpenSSL 라이브러리를 사용합니다. 다음 표에서는 최소 지원되는 버전의 OpenSSL 및 각 플랫폼에 대한 기본 인증서 신뢰 저장소 위치를 보여 줍니다.

|플랫폼|최소 OpenSSL 버전|기본 인증서 신뢰 저장소 위치|  
|------------|---------------------------|--------------------------------------------|
|Debian 8.71 |1.0.1t|/etc/ssl/certs|
|macOS 10.12|1.0.2k|/usr/local/etc/openssl/certs|
|OS X 10.11|1.0.2j|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|  
|Red Hat Enterprise Linux 7|1.0.1e|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1i|/etc/ssl/certs|
|Ubuntu 15.10 |1.0.2d|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2g|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2g|/etc/ssl/certs|
  
암호화를 사용 하 여 연결 문자열에 지정할 수도 있습니다는 `Encrypt` 옵션을 사용 하는 경우 **SQLDriverConnect** 연결 합니다.

## <a name="see-also"></a>관련 항목:  
[Microsoft ODBC Driver for Linux와 macOS에서 SQL Server 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)

