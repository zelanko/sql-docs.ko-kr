---
title: Linux에서 SQL Server 연결 암호화 | Microsoft Docs
description: 이 문서는 Linux에서 SQL Server 연결 암호화를 설명합니다.
author: tmullaney
ms.date: 01/30/2018
ms.author: meetb
manager: craigg
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: 933a3d2b59af1c9f794b286d535386fbeac31f73
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Linux에서 SQL Server 연결 암호화

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Linux 수를 사용 하 여 보안 TLS (전송 계층)의 인스턴스와 클라이언트 응용 프로그램 간에 네트워크를 통해 전송 되는 데이터를 암호화 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Windows와 Linux 모두에서 동일한 TLS 프로토콜을 지원: TLS 1.2, 1.1 및 1.0입니다. 그러나 TLS를 구성 하는 단계는 운영 체제를 관련이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 실행 합니다.  

## <a name="requirements-for-certificates"></a>인증서에 대 한 요구 사항 
시작 하기 전에 인증서를 이러한 요구 사항을 수행 되도록 해야 합니다.
- 현재 시스템 시간을 인증서의 속성 및 유효 기간 전에 인증서의 속성에서 유효 기간 이후 여야 합니다.
- 인증서는 서버 인증용이어야 합니다. 이 서버 인증 (1.3.6.1.5.5.7.3.1)을 지정 하려면 인증서의 확장 된 키 사용 속성이 필요 합니다.
- 인증서에 AT_KEYEXCHANGE KeySpec 옵션을 사용 하 여 만들어야 합니다. 일반적으로 인증서의 키 용도 속성 (KEY_USAGE) 키 암호화 (CERT_KEY_ENCIPHERMENT_KEY_USAGE)도 포함 됩니다.
- 인증서의 주체 속성과 CN (일반 이름) 호스트 이름이 나 서버 컴퓨터의 정규화 된 도메인 이름 (FQDN)으로 동일한 인지 지정 해야 합니다. 참고: 와일드 카드 인증서 지원 됩니다. 

## <a name="overview"></a>개요
TLS를 사용 하 여 클라이언트 응용 프로그램에서 연결을 암호화 하 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 올바르게 구성 된 경우 개인 정보 및 클라이언트와 서버 간의 통신에 대 한 데이터 무결성 모두 TLS를 제공 합니다.  TLS 연결의 시작 하는 클라이언트 또는 서버에서 시작 된 일 수 있습니다. 


## <a name="client-initiated-encryption"></a>클라이언트는 암호화 시작 
- **인증서 생성** (/CN와 일치 해야 SQL Server 호스트 정규화 된 도메인 이름)

> [!NOTE]
> 이 예제에서는 자체 서명 된 인증서 사용에 대 한이 쓰일 수 없습니다 프로덕션 시나리오에 있습니다. CA 인증서를 사용 해야 합니다. 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **SQL Server 구성**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **(Windows, Linux 또는 macOS) 클라이언트 컴퓨터의 인증서 등록**

    -   CA 서명된 인증서를 사용 하는 경우 클라이언트 컴퓨터에는 사용자 인증서 대신 CA (인증 기관) 인증서를 복사 해야 합니다. 
    -   자체 서명 된 인증서를 사용 하는 경우 방금.pem 파일을 배포 각각 다음 폴더에 복사 및 사용할 수 있도록 하기 위해 명령 실행 
        - **Ubuntu**: 인증서를 복사 ```/usr/share/ca-certificates/``` .crt에 이름 바꾸기 확장 dpkg reconfigure ca 인증서를 사용 하 여 시스템 CA 인증서로 사용 하도록 설정 합니다. 
        - **RHEL**: 인증서를 복사 ```/etc/pki/ca-trust/source/anchors/``` 사용 ```update-ca-trust``` 시스템 CA 인증서로 사용 하도록 설정 합니다.
        - **SUSE**: 인증서를 복사 ```/usr/share/pki/trust/anchors/``` 사용 ```update-ca-certificates``` 시스템 CA 인증서로 사용 하도록 설정 합니다.
        - **Windows**:-> 인증서 루트 인증 기관 트러스트 된-> 현재 사용자 인증서로.pem 파일 가져오기
        - **macOS**: 
           - 인증서를 복사 합니다. ```/usr/local/etc/openssl/certs```
           - 해시 값을 가져오려면 다음 명령을 실행 합니다. ```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - 값은 인증서를 이름을 바꿉니다. 예를 들면 ```mv mssql.pem dc2dd900.0```과 같습니다. Dc2dd900.0에 있는지 확인 ```/usr/local/etc/openssl/certs```
    
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

## <a name="server-initiated-encryption"></a>서버 암호화 시작 

- **인증서 생성** (/CN와 일치 해야 SQL Server 호스트 정규화 된 도메인 이름)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **SQL Server 구성**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key 
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
> 설정 **TrustServerCertificate** 클라이언트 인증서의 신뢰성을 확인 하는 CA에 연결할 수 없는 경우 True로

## <a name="common-connection-errors"></a>일반적인 연결 오류  

|오류 메시지입니다. |Fix |
|--- |--- |
|인증서 체인은 신뢰할 수 없는 기관에서 발급 되었습니다.  |이 오류는 클라이언트가 TLS 핸드셰이크 중에 SQL Server에서 제공 하는 인증서의 서명을 확인할 수 없는 경우에 발생 합니다. 클라이언트에서 신뢰 하거나 있는지 확인은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증서를 직접 또는 SQL Server 인증서를 서명한 CA입니다. |
|대상 보안 주체 이름이 올바르지 않습니다.  |SQL Server의 인증서 일반 이름 필드는 클라이언트의 연결 문자열에 지정 된 서버 이름과 일치 하는지 확인 합니다. |  
|현재 연결은 원격 호스트에 의해 강제로 끊겼습니다. |클라이언트가 SQL Server에 필요한 TLS 프로토콜 버전을 지원 하지 않습니다이 오류가 발생할 수 있습니다. 예를 들어 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] TLS 1.2 필요, 클라이언트도 TLS 1.2 프로토콜을 지원 하는지 확인 하도록 구성 되어 있습니다. |
| | |   
