---
title: 통합 인증 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 834ec3118685da8059999b3986af3edb39dc3e58
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042252"
---
# <a name="using-integrated-authentication"></a>통합 인증 사용
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux 및 macOS 기반 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 Kerberos 통합된 인증을 사용하는 연결을 지원합니다. MIT Kerberos KDC(키 배포 센터)를 지원하고 GSSAPI(Generic Security Services Application Program Interface) 및 Kerberos v5 라이브러리를 사용하여 작동합니다.
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversion-mdmd-from-an-odbc-application"></a>통합 인증을 사용하여 ODBC 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결  

**SQLDriverConnect** 또는 **SQLConnect**의 연결 문자열에서 **Trusted_Connection = yes**를 지정하여 Kerberos 통합 인증을 사용하도록 설정할 수 있습니다. 예를 들어  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
DSN과 연결하는 경우 `odbc.ini`의 DSN 항목에 **Trusted_Connection = yes**를 추가할 수도 있습니다.
  
또한 `sqlcmd`의 `-E` 옵션 및 `bcp`의 `-T`을 사용하여 통합 인증을 지정할 수 있습니다. 자세한 내용은 [**sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)를 사용하여 연결 및 [**bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)를 사용하여 연결을 참조하세요.

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 클라이언트 보안 주체가 이미 Kerberos KDC로 인증되었는지 확인합니다.
  
**ServerSPN** 및 **FailoverPartnerSPN** 이 지원되지 않습니다.  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>서비스로 실행하도록 설계된 Linux 또는 macOS ODBC Driver 애플리케이션 배포

시스템 관리자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하기 위해 Kerberos 인증을 사용하는 서비스로 실행하도록 애플리케이션을 배포할 수 있습니다.  
  
먼저 클라이언트에서 Kerberos를 구성한 다음, 애플리케이션이 기본 보안 주체의 Kerberos 자격 증명을 사용할 수 있도록 해야 합니다.

다음 방법 중 하나를 통해 연결에서 사용하는 보안 주체에 대해 TGT를 얻고 캐시하도록 `kinit` 또는 PAM(플러그형 인증 모듈)을 사용해야 합니다.  
  
-   `kinit`를 실행하여 보안 주체 이름 및 암호를 전달합니다.  
  
-   `kinit`를 실행하여 `ktutil`이 만든 보안 주체의 키를 포함하는 keytab 파일의 위치 및 보안 주체의 이름을 전달합니다.  
  
-   시스템에 대한 로그인이 Kerberos PAM(플러그형 인증 모듈)을 사용하여 수행되었는지 확인합니다.

Kerberos 자격 증명이 설계에 따라 만료되므로 애플리케이션이 서비스로 실행되는 경우 계속해서 서비스 가용성을 보장하도록 자격 증명을 갱신합니다. ODBC 드라이버는 자격 증명 자체를 갱신하지 않으며, 만료되기 전에 주기적으로 실행하여 자격 증명을 갱신하는 `cron` 작업 또는 스크립트가 있는지 확인합니다. 각 갱신마다 암호를 요구하지 않도록 keytab 파일을 사용할 수 있습니다.  
  
[Kerberos 구성 및 사용](https://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) 은 Linux에서 서비스를 Kerberize하는 방법에 대해 자세하게 설명합니다.
  
## <a name="tracking-access-to-a-database"></a>데이터베이스에 대한 액세스 추적

시스템 계정을 사용할 때 데이터베이스 관리자는 데이터베이스에 대한 액세스의 감사 내역을 만들어 통합 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 액세스할 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 로그인할 때 시스템 계정을 사용하고 보안 컨텍스트를 가장하기 위한 Linux 기능은 없습니다. 그러므로 사용자를 확인하기 위해 필요한 작업이 더 이상 없습니다.
  
시스템 계정이 아닌 사용자 대신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 활동을 감사하려면 애플리케이션이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE AS**를 사용해야 합니다.  
  
애플리케이션 성능을 향상하려면 애플리케이션이 통합 인증 및 감사를 사용하는 연결 풀링을 사용하면 됩니다. 그러나 연결 풀링, 통합 인증 및 감사를 함께 사용하면 unixODBC 드라이버 관리자가 서로 다른 사용자에게 풀링 연결을 다시 사용하도록 허용하기 때문에 보안 위험이 생깁니다. 자세한 내용은 [ODBC 연결 풀링](http://www.unixodbc.org/doc/conn_pool.html)을 참조하세요.  

다시 사용하기 전에 `sp_reset_connection`을 실행하여 애플리케이션이 풀링 연결을 다시 설정해야 합니다.  

## <a name="using-active-directory-to-manage-user-identities"></a>Active Directory를 사용하여 사용자 ID 관리

애플리케이션 시스템 관리자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 별도의 로그인 자격 증명 집합을 관리할 필요가 없습니다. 통합 인증에 대한 KDC(키 배포 센터)로 Active Directory를 구성할 수 있습니다. 자세한 내용은 [Microsoft Kerberos](/windows/desktop/SecAuthN/microsoft-kerberos)를 참조하세요.

## <a name="using-linked-server-and-distributed-queries"></a>연결된 서버 및 분산 쿼리 사용

개발자는 별도의 SQL 자격 증명 집합을 유지하는 데이터베이스 관리자 없이 연결된 서버 또는 분산 쿼리를 사용하는 애플리케이션을 배포할 수 있습니다. 이 경우 개발자는 통합된 인증을 사용하기 위해 애플리케이션을 구성해야 합니다.  
  
-   사용자는 클라이언트 컴퓨터에 로그인하고 애플리케이션 서버의 인증을 받습니다.  
  
-   애플리케이션 서버를 다른 데이터베이스로 인증하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 은 다른 데이터베이스에 데이터베이스 사용자로 인증합니다([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
통합된 인증을 구성한 후 자격 증명이 연결된 서버에 전달됩니다.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>통합 인증 및 sqlcmd
통합 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 액세스하려면 `sqlcmd`의 `-E` 옵션을 사용합니다. `sqlcmd`를 실행하는 계정이 기본 Kerberos 클라이언트 보안 주체와 연결되었는지 확인합니다.

## <a name="integrated-authentication-and-bcp"></a>통합 인증 및 bcp
통합 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 액세스하려면 `bcp`의 `-T` 옵션을 사용합니다. `bcp`를 실행하는 계정이 기본 Kerberos 클라이언트 보안 주체와 연결되었는지 확인합니다. 
  
`-T`를 `-U` 또는 `-P` 옵션과 함께 사용하는 것은 오류입니다.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 등록한 SPN에 대해 지원되는 구문

SPN이 연결 문자열 또는 연결 특성에서 사용하는 구문은 다음과 같습니다.  

|구문|설명|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|TCP가 사용될 때 공급자가 생성하는 기본 SPN입니다. *port* 는 TCP 포트 번호입니다. *fqdn* 은 정규화된 도메인 이름입니다.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Active Directory를 사용하여 Linux 또는 macOS 컴퓨터 인증

Kerberos를 구성하려면 `krb5.conf` 파일에 데이터를 입력합니다. `krb5.conf` `/etc/`에 있지만 구문(예: `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`)을 사용하여 다른 파일을 참조할 수 있습니다. 다음은 `krb5.conf` 파일의 예입니다.  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
```  
  
Linux 또는 macOS 컴퓨터가 사용할 DNS 서버를 제공하는 Windows DHCP 서버에서 DHCP(Dynamic Host Configuration Protocol)를 사용하도록 구성된 경우 **dns_lookup_kdc=true**를 사용할 수 있습니다. 이제 `kinit alias@YYYY.CORP.CONTOSO.COM` 명령을 실행하면 Kerberos를 사용하여 도메인에 로그인할 수 있습니다. `kinit`에 전달된 매개 변수는 대/소문자를 구분하며 도메인에 있도록 구성된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 컴퓨터에서 해당 사용자 `alias@YYYY.CORP.CONTOSO.COM`을 로그인 대상으로 추가했어야 합니다. 이제 신뢰할 수 있는 연결(연결 문자열의**Trusted_Connection=YES**, **bcp -T** 또는 **sqlcmd -E**)을 사용할 수 있습니다.  
  
Linux 또는 macOS 컴퓨터의 시간과 KDC Kerberos KDC(Key Distribution Center)의 시간이 비슷해야 합니다. NTP(Network Time Protocol)를 사용하여 시스템 시간이 올바르게 설정되었는지 확인합니다.  

Kerberos 인증이 실패하는 경우 Linux 또는 macOS 기반 ODBC 드라이버가 NTLM 인증을 사용하지 않습니다.  

Active Directory를 사용하여 Linux 또는 macOS 컴퓨터 인증에 대한 자세한 내용은 [Active Directory를 사용하여 Linux 인증](https://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) 및 [OS X와 Active Directory 통합 모범 사례](https://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)를 참조하세요. Kerberos 구성에 대한 자세한 내용은 [MIT Kerberos 설명서](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html)를 참조하세요.

## <a name="see-also"></a>참고 항목  
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)

[Azure Active Directory 사용](../../../connect/odbc/using-azure-active-directory.md)
