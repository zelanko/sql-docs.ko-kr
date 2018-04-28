---
title: 통합된 인증을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- integrated authentication
ms.assetid: 9499ffdf-e0ee-4d3c-8bca-605371eb52d9
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: edc89fa38ae3b4554f44290cf36073d6c6a0625b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-integrated-authentication"></a>통합 인증 사용
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Kerberos를 사용 하는 Linux 및 macOS 지원 연결에서 통합 인증입니다. MIT Kerberos 키 배포 센터 (KDC)를 지원 하 고 서비스 응용 프로그램 프로그램 인터페이스 GSSAPI (Generic Security) 및 Kerberos v5 라이브러리와 함께 작동 합니다.
  
## <a name="using-integrated-authentication-to-connect-to-includessnoversionincludesssnoversionmdmd-from-an-odbc-application"></a>통합된 인증을 사용 하 여 연결할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ODBC 응용 프로그램에서  

지정 하 여 Kerberos 통합된 인증을 사용할 수 있습니다 **Trusted_Connection = yes** 의 연결 문자열에 **SQLDriverConnect** 또는 **SQLConnect**합니다. 예를 들어:  

```
Driver='ODBC Driver 13 for SQL Server';Server=your_server;Trusted_Connection=yes  
```
  
DSN에 연결할 때 추가할 수도 있습니다 **Trusted_Connection = yes** 의 DSN 항목에 `odbc.ini`합니다.
  
`-E` 옵션의 `sqlcmd` 및 `-T` 옵션의 `bcp` 통합된 인증을 지정 하려면 사용할 수도 있습니다; 참조 [연결과 **sqlcmd** ](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md) 및 [ 사용 하 여 연결 **bcp** ](../../../connect/odbc/linux-mac/connecting-with-bcp.md) 자세한 정보에 대 한 합니다.

에 연결 하려는 클라이언트 보안 주체를 확인 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 가 이미 Kerberos KDC로 인증 되었습니다.
  
**ServerSPN** 및 **FailoverPartnerSPN** 이 지원되지 않습니다.  
  
## <a name="deploying-a-linux-or-macos-odbc-driver-application-designed-to-run-as-a-service"></a>Linux 또는 ODBC 드라이버 응용 프로그램 설계 macOS 실행을 위해 서비스로 배포 하기

시스템 관리자에 연결에 Kerberos 인증을 사용 하는 서비스로 실행 되도록 응용 프로그램을 배포할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
먼저 클라이언트 컴퓨터에서 Kerberos를 구성 하 고 다음 응용 프로그램이 기본 보안 주체의 Kerberos 자격 증명을 사용할 수 있는지 확인 해야 합니다.

사용 해야 `kinit` 또는 PAM (플러그형 인증 모듈)을 얻고 다음 방법 중 하나를 통해 연결에 사용 되는 보안 주체에 대 한 TGT 캐시:  
  
-   실행 `kinit`, 사용자 이름 및 암호를 전달 합니다.  
  
-   실행 `kinit`계정 이름 및에서 만든 보안 주체의 키를 포함 하는 keytab 파일의 위치를 전달, `ktutil`합니다.  
  
-   시스템에 로그인 했는지 확인 하십시오. Kerberos PAM (플러그형 인증 모듈)을 사용 하 여 합니다.

Kerberos 자격 증명으로 설계 만료 되므로 응용 프로그램을 서비스로 실행 하는 경우 지속적인된 서비스 가용성을 보장 하는 데 사용할 자격 증명을 갱신 합니다. ODBC 드라이버를 갱신 하지 않으면 자격 증명 자체; 있는지 확인 하는 `cron` 작업 또는 정기적으로 만료 되기 전에 자격 증명을 실행 하는 스크립트입니다. 각 갱신 마다 암호를 요구를 방지 하려면는 keytab 파일을 사용할 수 있습니다.  
  
[Kerberos 구성 및 사용](http://commons.oreilly.com/wiki/index.php/Linux_in_a_Windows_World/Centralized_Authentication_Tools/Kerberos_Configuration_and_Use) 은 Linux에서 서비스를 Kerberize하는 방법에 대해 자세하게 설명합니다.
  
## <a name="tracking-access-to-a-database"></a>데이터베이스에 대한 액세스 추적

시스템 계정을 사용 하 여 액세스 하는 경우 데이터베이스 관리자가 데이터베이스에 대 한 액세스 감사 내역을 만들 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 통합 인증을 사용 합니다.  
  
에 로그인 하기 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 시스템 계정을 사용 하 고 보안 컨텍스트를 가장할 linux 기능은 없습니다. 그러므로 사용자를 확인하기 위해 필요한 작업이 더 이상 없습니다.
  
활동을 감사 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 시스템 계정 이외의 사용자를 대신 하 여 응용 프로그램 사용 해야 [!INCLUDE[tsql](../../../includes/tsql_md.md)] **EXECUTE AS**합니다.  
  
응용 프로그램 성능을 향상하려면 응용 프로그램이 통합 인증 및 감사를 사용하는 연결 풀링을 사용하면 됩니다. 그러나 연결 풀링, 통합 인증 및 감사 결합 unixODBC 드라이버 관리자 풀링된 연결을 다시 사용을 다른 사용자가 허용 하기 때문에 보안 위험이 생깁니다. 자세한 내용은 [ODBC 연결 풀링](http://www.unixodbc.org/doc/conn_pool.html)을 참조하세요.  

재사용 하기 전에 응용 프로그램을 다시 설정 해야 풀링된 연결을 실행 하 여 `sp_reset_connection`합니다.  

## <a name="using-active-directory-to-manage-user-identities"></a>Active Directory를 사용하여 사용자 ID 관리

응용 프로그램 시스템 관리자는 별도 집합에 대 한 로그인 자격 증명을 관리 하지 않아도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. 통합 인증에 대한 KDC(키 배포 센터)로 Active Directory를 구성할 수 있습니다. 참조 [Microsoft Kerberos](https://msdn.microsoft.com/en-us/library/windows/desktop/aa378747(v=vs.85).aspx) 자세한 정보에 대 한 합니다.

## <a name="using-linked-server-and-distributed-queries"></a>연결된 서버 및 분산 쿼리 사용

개발자는 별도의 SQL 자격 증명 집합을 유지하는 데이터베이스 관리자 없이 연결된 서버 또는 분산 쿼리를 사용하는 응용 프로그램을 배포할 수 있습니다. 이 경우 개발자는 통합된 인증을 사용 하도록 응용 프로그램을 구성 해야 합니다.  
  
-   사용자는 클라이언트 컴퓨터에 로그인하고 응용 프로그램 서버의 인증을 받습니다.  
  
-   응용 프로그램 서버를 다른 데이터베이스로 인증 하 고 연결할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 다른 데이터베이스에 데이터베이스 사용자로 인증 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
통합된 인증을 구성한 후 자격 증명이 연결된 서버에 전달됩니다.  
  
## <a name="integrated-authentication-and-sqlcmd"></a>통합 인증 및 sqlcmd
에 액세스 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 통합된 인증을 사용 하 여는 `-E` 옵션의 `sqlcmd`합니다. 실행 계정이 확인 `sqlcmd` 기본 Kerberos 클라이언트 보안 주체와 연결 됩니다.

## <a name="integrated-authentication-and-bcp"></a>통합 인증 및 bcp
에 액세스 하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 통합된 인증을 사용 하 여는 `-T` 옵션의 `bcp`합니다. 실행 계정이 확인 `bcp` 기본 Kerberos 클라이언트 보안 주체와 연결 됩니다. 
  
사용 하면 오류가 발생 `-T` 와 `-U` 또는 `-P` 옵션입니다.
  
## <a name="supported-syntax-for-an-spn-registered-by-includessnoversionincludesssnoversionmdmd"></a>가 등록 한 SPN에 대 한 지원 되는 구문 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]

Spn이 연결 문자열이 나 연결 특성에서 사용 하는 구문은 다음과 같습니다.  

|구문|Description|  
|----------|---------------|  
|MSSQLSvc/*fqdn*:*port*|TCP가 사용될 때 공급자가 생성하는 기본 SPN입니다. *port* 는 TCP 포트 번호입니다. *fqdn* 은 정규화된 도메인 이름입니다.|  
  
## <a name="authenticating-a-linux-or-macos-computer-with-active-directory"></a>Linux 또는 macOS Active Directory를 사용 하 여 컴퓨터를 인증합니다.

Kerberos를 구성 하려면 데이터를 입력할는 `krb5.conf` 파일입니다. `krb5.conf` 에 `/etc/` 예: 구문을 사용 하 여 다른 파일을 참조할 수 있습니다 하지만 `export KRB5_CONFIG=/home/dbapp/etc/krb5.conf`합니다. 다음은 예제 `krb5.conf` 파일:  
  
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
  
를 사용 하도록 DNS 서버를 제공 하는 Windows DHCP 서버와 동적 호스트 구성 프로토콜 (DHCP)를 사용 하도록 프로그램 Linux 또는 macOS 컴퓨터 구성 된 경우 사용할 수 있습니다 **dns_lookup_kdc = true**합니다. Kerberos를 사용 하 여 명령을 실행 하 여 도메인에 로그인 할 수 이제 `kinit alias@YYYY.CORP.CONTOSO.COM`합니다. 매개 변수가 전달 `kinit` 대/소문자 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 도메인에 포함 되도록 구성 된 컴퓨터에는 해당 사용자 있어야 `alias@YYYY.CORP.CONTOSO.COM` 로그인에 대 한 추가 합니다. 이제, 신뢰할 수 있는 연결을 사용할 수 있습니다 (**Trusted_Connection = YES** 연결 문자열에 **bcp-T**, 또는 **sqlcmd-E**).  
  
Linux 또는 macOS 컴퓨터와 Kerberos 키 배포 센터 (KDC)에 시간 종료 해야 합니다. 시스템 시간이 올바르게 설정 되어 있는지, 예를 들어 (NTP (Network Time Protocol)를 사용 하 여 확인 합니다.  

Kerberos 인증에 실패 하면 macOS 또는 Linux 기반 ODBC 드라이버가 NTLM 인증을 사용 하지 않습니다.  

Active Directory와 macOS 또는 Linux 컴퓨터를 인증 하는 방법에 대 한 자세한 내용은 참조 [Active Directory로 Linux 클라이언트 인증](http://technet.microsoft.com/magazine/2008.12.linux.aspx#id0060048) 및 [ActiveDirectory와통합OSX에대한모범사례](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf). Kerberos 구성에 대 한 자세한 내용은 참조는 [MIT Kerberos 설명서](https://web.mit.edu/kerberos/krb5-1.12/doc/index.html)합니다.

## <a name="see-also"></a>관련 항목:  
[프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)

[Azure Active Directory를 사용 하 여](../../../connect/odbc/using-azure-active-directory.md)
