---
title: 암호화를 사용하여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cff4228404690147d97a44f6f5dd43b1a180153c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "71713289"
---
# <a name="connecting-with-encryption"></a>암호화를 사용하여 연결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 문서의 예제에서는 애플리케이션이 Java 애플리케이션에서 TLS(전송 계층 보안) 암호화를 사용할 수 있도록 하는 연결 문자열 속성을 사용하는 방법에 대해 설명합니다. **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** 및 **hostNameInCertificate** 등의 새 연결 문자열 속성에 대한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
 **encrypt** 속성이 **true**로 설정되고 **trustServerCertificate** 속성이 **true**로 설정되어 있는 경우 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TLS 인증서의 유효성을 검사하지 않습니다. 이 설정은 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 자체 서명된 인증서만 있는 경우와 같이 테스트 환경에서 연결을 허용하는 데 필요합니다.  
  
 다음 코드 예제에서는 연결 문자열에 **trustServerCertificate** 속성을 설정하는 방법을 보여 줍니다.  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 **encrypt** 속성이 **true**로 설정되고 **trustServerCertificate** 속성이 **true**로 설정되어 있는 경우 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TLS 인증서의 유효성을 검사하지 않습니다. 서버 인증서의 유효성 검사는 TLS 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 서버 인증서의 유효성을 검사하려면 명시적으로 **trustStore** 및 **trustStorePassword** 연결 속성을 사용하거나 암시적으로 기본 JVM(Java Virtual Machine)의 기본 트러스트 저장소를 사용하여 연결 시에 트러스트 자료를 제공해야 합니다.  
  
 **trustStore** 속성은 클라이언트에서 신뢰하는 인증서 목록이 포함되어 있는 인증서 trustStore 파일에 대한 경로(파일 이름 포함)를 지정합니다. **trustStorePassword** 속성은 trustStore 데이터의 무결성을 검사하는 데 사용되는 암호를 지정합니다. JVM의 기본 트러스트 저장소를 사용하는 방법은 [암호화에 대한 클라이언트 구성](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)을 참조하세요.  
  
 다음 코드 예제에서는 연결 문자열에 **trustStore** 및 **trustStorePassword** 속성을 설정하는 방법을 보여 줍니다.  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 JDBC 드라이버는 **hostNameInCertificate**라는 속성을 추가로 제공하는데 이 속성은 서버의 호스트 이름을 지정합니다. 이 속성의 값은 인증서의 주체 속성과 일치해야 합니다.  
  
 다음 코드 예제는 연결 문자열에서 **hostNameInCertificate** 속성을 사용하는 방법을 보여 줍니다.  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  또는 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스에서 제공하는 적절한 **setter** 메서드를 사용하여 연결 속성의 값을 설정할 수 있습니다.  
  
 **encrypt** 속성이 **true**로 설정되고 **trustServerCertificate** 속성이 **false**로 설정되며 연결 문자열의 서버 이름이 TLS 인증서의 서버 이름과 일치하지 않는 경우 다음 오류가 발생합니다. `The driver couldn't establish a secure connection to SQL Server by using Secure Sockets Layer (SSL) encryption. Error: "java.security.cert.CertificateException: Failed to validate the server name in a certificate during Secure Sockets Layer (SSL) initialization."`. 버전 7.2부터 드라이버는 TLS 인증서에 있는 서버 이름의 맨 왼쪽 레이블에서 와일드카드 패턴 일치를 지원합니다.

## <a name="see-also"></a>참고 항목

 [암호화 사용](../../connect/jdbc/using-ssl-encryption.md) [JDBC 드라이버 애플리케이션 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)