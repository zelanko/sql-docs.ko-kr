---
title: SQL Server on Linux에 대한 연결 암호화
description: 이 문서에서는 SQL Server on Linux에 대한 연결 암호화를 설명합니다.
ms.date: 01/30/2018
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: 975a312988a7df4bdb4fb2858d7b0fcbe95cea33
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71016858"
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>SQL Server on Linux에 대한 연결 암호화

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] on Linux에서는 TLS(전송 계층 보안)를 사용하여 클라이언트 애플리케이션과 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 간에 네트워크를 통해 전송되는 데이터를 암호화할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 Windows 및 Linux에서 동일한 TLS 프로토콜인 TLS 1.2, 1.1 및 1.0을 지원합니다. 그러나 TLS를 구성하는 단계는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 실행되는 운영 체제에만 해당합니다.  

## <a name="requirements-for-certificates"></a>인증서 요구 사항 
시작하기 전에 인증서가 다음 요구 사항을 준수하는지 확인해야 합니다.
- 현재 시스템 시간은 인증서의 유효 기간(시작) 속성 이후이고 인증서의 유효 기간(끝) 속성 이전이어야 합니다.
- 인증서는 서버 인증용이어야 합니다. 이를 위해서는 인증서의 확장된 키 사용 속성으로 서버 인증(1.3.6.1.5.5.7.3.1)을 지정해야 합니다.
- 인증서는 AT_KEYEXCHANGE의 KeySpec 옵션을 사용하여 만들어야 합니다. 일반적으로 인증서의 키 사용 속성(KEY_USAGE)에는 키 암호화(CERT_KEY_ENCIPHERMENT_KEY_USAGE)도 포함됩니다.
- 인증서의 주체 속성은 CN(일반 이름)이 서버 컴퓨터의 호스트 이름이나 FQDN(정규화된 도메인 이름)과 동일함을 나타내야 합니다. 참고: 와일드카드 인증서가 지원됩니다.

## <a name="configuring-the-openssl-libraries-for-use-optional"></a>사용할 OpenSSL 라이브러리 구성(선택 사항)
`/opt/mssql/lib/` 디렉터리에서 암호화에 사용할 `libcrypto.so` 및 `libssl.so` 라이브러리를 참조하는 바로 가기 링크를 만들 수 있습니다. 이 링크는 SQL Server에서 시스템이 제공하는 기본값이 아닌 OpenSSL의 특정 버전을 사용하도록 하려는 경우 유용합니다. 이 바로 가기 링크가 없으면 SQL Server는 시스템에 구성된 기본 OpenSSL 라이브러리를 로드합니다.

이 바로 가기 링크는 이름을 `libcrypto.so` 및 `libssl.so`로 지정하고 `/opt/mssql/lib/` 디렉터리에 배치해야 합니다.

## <a name="overview"></a>개요
TLS는 클라이언트 애플리케이션에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 연결을 암호화하는 데 사용됩니다. 올바르게 구성된 경우 TLS는 클라이언트와 서버 간 통신에 대한 프라이버시 및 데이터 무결성을 모두 제공합니다.  TLS 연결은 클라이언트에서 시작되거나 서버에서 시작될 수 있습니다. 

## <a name="client-initiated-encryption"></a>클라이언트 시작 암호화 
- **인증서 생성**(/CN은 SQL Server 호스트의 정규화된 도메인 이름과 일치해야 함)

> [!NOTE]
> 이 예제에서는 자체 서명된 인증서를 사용합니다. 프로덕션 시나리오에는 이 인증서를 사용하면 안 됩니다. CA 인증서를 사용해야 합니다. 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **SQL Server 구성**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **클라이언트 머신(Windows, Linux 또는 macOS)에 인증서 등록**

    -   CA 서명 인증서를 사용하는 경우 사용자 인증서 대신 CA(인증 기관) 인증서를 클라이언트 머신에 복사해야 합니다. 
    -   자체 서명된 인증서를 사용하는 경우 배포에 대해 각각 다음 폴더에 .pem 파일을 복사하고 명령을 실행하여 사용하도록 설정합니다. 
        - **Ubuntu**: 인증서를 ```/usr/share/ca-certificates/```에 복사하고, 확장명을 .crt로 변경하고, dpkg-reconfigure ca-certificates를 사용하여 시스템 CA 인증서로 사용하도록 설정합니다. 
        - **RHEL**: 인증서를 ```/etc/pki/ca-trust/source/anchors/```에 복사하고 ```update-ca-trust```를 사용하여 시스템 CA 인증서로 사용하도록 설정합니다.
        - **SUSE**: 인증서를 ```/usr/share/pki/trust/anchors/```에 복사하고 ```update-ca-certificates```를 사용하여 시스템 CA 인증서로 사용하도록 설정합니다.
        - **Windows**:  [현재 사용자] -> [신뢰할 수 있는 루트 인증 기관] -> [인증서]에서 .pem 파일을 인증서로 가져옵니다.
        - **macOS**: 
           - 인증서를 ```/usr/local/etc/openssl/certs```에 복사합니다.
           - 다음 명령을 실행하여 해시 값 ```/usr/local/Cellar/openssl/1.0.2l/openssl x509 -hash -in mssql.pem -noout```를 가져옵니다.
           - 인증서의 이름을 value로 바꿉니다. 예: ```mv mssql.pem dc2dd900.0``` dc2dd900.0이 ```/usr/local/etc/openssl/certs```에 있는지 확인합니다.
    
-   **연결 문자열 예** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![SSMS 연결 대화 상자](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS 연결 대화 상자")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>서버 시작 암호화 

- **인증서 생성**(/CN은 SQL Server 호스트의 정규화된 도메인 이름과 일치해야 함)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **SQL Server 구성**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **연결 문자열 예** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> 클라이언트가 CA에 연결하여 인증서의 신뢰성을 검사할 수 없는 경우 **TrustServerCertificate**를 True로 설정합니다.

## <a name="common-connection-errors"></a>일반적인 연결 오류  

|오류 메시지 |Fix |
|--- |--- |
|인증서 체인이 신뢰할 수 없는 인증 기관으로부터 발급되었습니다.  |이 오류는 클라이언트가 TLS 핸드셰이크 중 SQL Server에서 제공하는 인증서의 서명을 확인할 수 없는 경우 발생합니다. 클라이언트가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증서를 직접 신뢰하거나 SQL Server 인증서에 서명한 CA를 신뢰하는지 확인합니다. |
|대상 보안 주체 이름이 잘못되었습니다.  |SQL Server 인증서의 일반 이름 필드가 클라이언트의 연결 문자열에 지정된 서버 이름과 일치하는지 확인합니다. |  
|현재 연결은 원격 호스트에 의해 강제로 끊겼습니다. |클라이언트에서 SQL Server에 필요한 TLS 프로토콜 버전을 지원하지 않는 경우 이 오류가 발생할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 TLS 1.2를 사용하도록 구성된 경우 클라이언트가 TLS 1.2 프로토콜도 지원하는지 확인합니다. |
| | |   
