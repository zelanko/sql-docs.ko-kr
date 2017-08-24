---
title: "Linux에서 SQL Server 연결 암호화 | Microsoft Docs"
description: "이 항목에서는 Linux에서 SQL Server 연결 암호화를 설명 합니다."
author: tmullaney
ms.date: 06/14/2017
ms.author: thmullan;rickbyh
manager: jhubbard
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
helpviewer_keywords:
- Linux, encrypted connections
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dfbfeee8292f3af4020185248d3d6a3fad3c71ea
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Linux에서 SQL Server 연결 암호화

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]Linux 수를 사용 하 여 보안 TLS (전송 계층)의 인스턴스와 클라이언트 응용 프로그램 간에 네트워크를 통해 전송 되는 데이터를 암호화 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]Windows와 Linux 모두에서 동일한 TLS 프로토콜을 지원: TLS 1.2, 1.1 및 1.0입니다. 그러나 TLS를 구성 하는 단계는 운영 체제를 관련이 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 실행 합니다.  
 
## <a name="typical-scenario"></a>일반적인 시나리오 
TLS를 사용 하 여 클라이언트 응용 프로그램에서 연결을 암호화 하 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]합니다. 올바르게 구성 된 경우 개인 정보 및 클라이언트와 서버 간의 통신에 대 한 데이터 무결성 모두 TLS를 제공 합니다.  
다음 단계에서는 일반적인 시나리오를 설명합니다.  

1. 데이터베이스 관리자는 개인 키와 인증서 서명 요청 (CSR)를 생성 합니다. CSR의 일반 이름에는 클라이언트가 해당 SQL Server 연결 문자열에 지정 된 서버 이름을 일치 해야 합니다. 이 일반 이름은 일반적으로의 정규화 된 도메인 이름입니다.는 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 호스트 합니다. 여러 서버에 대 한 동일한 인증서를 사용 하려면 일반 이름에 와일드 카드를 사용할 수 있습니다 (예를 들어 `"*.contoso.com"` 대신 `"node1.contoso.com"`).   
2. CSR 서명을 위해 인증 기관 (CA)에 전송 됩니다. CA에 연결 하는 모든 클라이언트 컴퓨터에서 신뢰 되어야 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]합니다. CA는 데이터베이스 관리자에 서명 된 인증서를 반환합니다.   
3. 데이터베이스 관리자는 구성 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] TLS 연결에 대 한 개인 키 및 서명 된 인증서를 사용 하도록 합니다.   
4. 클라이언트는 지정 `"Encrypt=True"` 및 `"TrustServerCertificate=False"` 은 연결 문자열에 있습니다. (특정 매개 변수 이름은 달라질 수 있습니다 사용할 드라이버를 사용 하는 따라)입니다. 이제 SQL Server에 대 한 연결을 암호화 하 고 중간자 개입 공격을 방지 하려면 SQL Server의 인증서의 유효성을 검사 하는 시도 클라이언트입니다.  
 
## <a name="configuring-tls-on-linux"></a>Linux에서 TLS를 구성합니다.  

사용 하 여 `mssql-conf` 의 인스턴스에 대 한 TLS를 구성 하려면 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] Linux에서 실행 합니다. 다음 옵션이 지원 됩니다.  

|옵션 |Description |
|--- |--- |
|`network.forceencryption` |1 인 경우, 다음 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 암호화에 대 한 모든 연결을 강제로 수행 합니다. 기본적으로이 옵션은 0입니다. |  
|`network.tlscert` |인증서에 절대 경로 파일 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] TLS를 사용 합니다. 예: `/etc/ssl/certs/mssql.pem` 인증서 파일 mssql 계정에서 액세스할 수 있어야 합니다. 사용 하 여 파일에 대 한 액세스를 제한 하는 것이 좋습니다 `chown mssql:mssql <file>; chmod 400 <file>`합니다. |  
|`network.tlskey` |개인 키에 절대 경로 파일 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] TLS를 사용 합니다. 예: `/etc/ssl/private/mssql.key` 인증서 파일 mssql 계정에서 액세스할 수 있어야 합니다. 사용 하 여 파일에 대 한 액세스를 제한 하는 것이 좋습니다 `chown mssql:mssql <file>; chmod 400 <file>`합니다. | 
|`network.tlsprotocols` |프로토콜은 SQL Server에서 허용 하는 TLS의 쉼표로 구분 된 목록입니다. [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]항상 가장 강력한 허용 된 프로토콜을 협상 하도록 시도 합니다. 클라이언트가 허용 된 모든 프로토콜을 지원 하지 않는 경우 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 연결 시도 거부 합니다.  호환성을 위해 지원 되는 모든 프로토콜은 기본 (1.2, 1.1, 1.0)에서 허용 됩니다.  TLS 1.2를 지원 하려면 클라이언트, TLS 1.2만을 허용 하는 것이 좋습니다. |  
|`network.tlsciphers` |허용 하는 암호 지정 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] TLS에 대 한 합니다. 이 문자열 당 포맷 해야 [OpenSSL의 암호화 목록 형식](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)합니다. 일반적으로이 옵션을 변경할 필요가 없습니다. <br /> 기본적으로 다음 암호 허용 됩니다. <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |   
| | |
 
## <a name="example"></a>예제 
이 예제에서는 자체 서명 된 인증서를 사용 합니다. 일반적인 프로덕션 시나리오에서 모든 클라이언트에서 신뢰 하는 CA에서 인증서를 서명 합니다.  
 
### <a name="step-1-generate-private-key-and-certificate"></a>1 단계: 개인 키와 인증서를 생성 합니다. 
Linux 컴퓨터에서 터미널 명령을 열고 여기서 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 실행 합니다. 다음 명령을 실행 합니다.  

- 자체 서명 된 인증서를 생성 합니다. /CN SQL Server 호스트 정규화 된 도메인 이름을 일치 하는지 확인 합니다. 사용할 수 있습니다 필요에 따라 와일드 카드, 예를 들어 `'/CN=*.contoso.com'`합니다.    
   ```  
   openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
   ```  

- 에 대 한 액세스를 제한 합니다.`mssql`  
   ```  
   sudo chown mssql:mssql mssql.pem mssql.key 
   sudo chmod 400 mssql.pem mssql.key 
   ```  
 
- 시스템 SSL 디렉터리 (선택 사항)으로 이동  
   ```  
   sudo mv mssql.pem /etc/ssl/certs/ 
   sudo mv mssql.key /etc/ssl/private/ 
   ```  
 
### <a name="step-2-configure--includessnoversiondocsincludesssnoversion-mdmd"></a>2 단계: 구성[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]  
사용 하 여 `mssql-conf` 구성 하려면 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 인증서를 사용 하 여 TLS에 대 한 키입니다. 보안 향상된을 위해 허용 되는 프로토콜 유일한으로 TLS 1.2를 설정 하 고 모든 클라이언트가 암호화 된 연결을 사용 하도록 강제 합니다.  

```  
sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
```
 
### <a name="step-3-restart-includessnoversiondocsincludesssnoversion-mdmd"></a>3 단계: 다시 시작[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 
[!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]이러한 변경 내용을 적용 하려면 다시 시작 해야 합니다.  
`sudo systemctl restart mssql-server`  
 
### <a name="step-4-copy-self-signed-certificate-to-client-machines"></a>4 단계: 클라이언트 컴퓨터에 자체 서명 된 인증서를 복사 
이 예제에서 자체 서명 인증서를 사용 하기 때문에 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 호스트 인증서 (개인 키가 아닌)를 복사 하 여에 연결 하는 모든 클라이언트 컴퓨터에서 신뢰할 수 있는 루트 인증서로 설치 해야 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)]합니다. 인증서에는 모든 클라이언트에서 이미 신뢰할 수 있는 CA에서 서명, 경우에이 단계가 필요 하지 않습니다. 
 
### <a name="step-5-connect-from-clients-using-tls"></a>5 단계: TLS를 사용 하는 클라이언트에서 연결 
연결할 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 암호화 사용을 사용 하 여 클라이언트에서 및 `TrustServerCertificate` 로 설정 `False` 연결 문자열에 있습니다. 다음은 다양 한 도구 및 드라이버를 사용 하 여 이러한 매개 변수를 지정 하는 방법의 몇 가지 예입니다. 

sqlcmd  
`sqlcmd -N -C -S mssql.contoso.com -U sa -P '<YourPassword>'`  

[!INCLUDE[ssmanstudiofull-md](../../docs/includes/ssmanstudiofull-md.md)]   
  ![SSMS 연결 대화 상자](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 연결 대화 상자")  
  
ADO.NET  
`"Encrypt=true; TrustServerCertificate=true;"`  

ODBC   
`"Encrypt=yes; TrustServerCertificate=no;"`  

JDBC  
`"encrypt=true; trustServerCertificate=false;" `

 
## <a name="common-connection-errors"></a>일반적인 연결 오류  

|오류 메시지입니다. |Fix |
|--- |--- |
|인증서 체인은 신뢰할 수 없는 기관에서 발급 되었습니다.  |이 오류는 클라이언트가 TLS 핸드셰이크 중에 SQL Server에서 제공 하는 인증서의 서명을 확인할 수 없는 경우에 발생 합니다. 클라이언트에서 신뢰 하거나 있는지 확인은 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] 인증서를 직접 또는 SQL Server 인증서를 서명한 CA입니다. |
|대상 보안 주체 이름이 올바르지 않습니다.  |SQL Server의 인증서 일반 이름 필드는 클라이언트의 연결 문자열에 지정 된 서버 이름과 일치 하는지 확인 합니다. |  
|현재 연결은 원격 호스트에 의해 강제로 끊겼습니다. |클라이언트가 SQL Server에 필요한 TLS 프로토콜 버전을 지원 하지 않습니다이 오류가 발생할 수 있습니다. 예를 들어 경우 [!INCLUDE[ssNoVersion](../../docs/includes/ssnoversion-md.md)] TLS 1.2 필요, 클라이언트도 TLS 1.2 프로토콜을 지원 하는지 확인 하도록 구성 되어 있습니다. |
| | |   


