---
title: SSL 암호화를 사용 하 여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49c6aaf771bb5335b8ba649869a4a8cf13894e82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832618"
---
# <a name="connecting-with-ssl-encryption"></a>SSL 암호화를 사용한 연결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 항목의 예제에서는 응용 프로그램이 Java 응용 프로그램에서 SSL(Secure Sockets Layer) 암호화를 사용할 수 있도록 하는 연결 문자열 속성을 사용하는 방법에 대해 설명합니다. 이러한 새 연결에 대 한 자세한 내용은 속성을와 같은 문자열 **암호화**, **trustServerCertificate**, **trustStore**,  **trustStorePassword**, 및 **hostNameInCertificate**, 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 때는 **암호화** 속성이 **true** 및 **trustServerCertificate** 속성이 **true**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 유효성을 검사 하지 것입니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 인증서입니다. 이 일반적으로 위치 등의 테스트 환경에서 연결을 허용 하는 데 필요는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 자체 서명 된 인증서만 합니다.  
  
 다음 코드 예제에서는 설정 하는 방법을 보여 줍니다.는 **trustServerCertificate** 는 연결 문자열의 속성:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 때는 **암호화** 속성이 **true** 및 **trustServerCertificate** 속성이 **false**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 유효성을 검사 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 인증서입니다. 서버 인증서의 유효성 검사는 SSL 핸드셰이크의 일부로 서버가 연결할 올바른 서버인지 확인합니다. 서버 인증서의 유효성을 검사 하기 위해 트러스트 자료를 사용 하 여 연결 시 제공 해야 **trustStore** 및 **trustStorePassword** 연결 속성 또는 명시적으로 사용 하 여 기본 가상 컴퓨터 JVM (Java)의 기본 트러스트는 암시적으로 저장 합니다.  
  
 **trustStore** 신뢰할 수 있는 인증서 목록이 포함 된 인증서 trustStore 파일 경로 (파일 이름 포함)를 지정 하는 속성입니다. **trustStorePassword** 속성 trustStore 데이터의 무결성을 확인 하는 데 사용 하는 암호를 지정 합니다. JVM의 기본 트러스트 저장소를 사용 하 여에 자세한 내용은 참조는 [SSL 암호화를 위한 클라이언트 구성](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)합니다.  
  
 다음 코드 예제에서는 설정 하는 방법을 보여 줍니다.는 **trustStore** 및 **trustStorePassword** 연결 문자열에는 속성:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 JDBC 드라이버는 추가 속성을 **hostNameInCertificate**, 서버의 호스트 이름을 지정 합니다. 이 속성의 값은 인증서의 주체 속성과 일치해야 합니다.  
  
 다음 코드 예제에서는 사용 하는 방법을 보여 줍니다.는 **hostNameInCertificate** 는 연결 문자열의 속성:  
  
```  
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  적절 한 사용 하 여 연결 속성의 값을 설정할 수 또는 **setter** 에서 제공 하는 메서드는 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스입니다.  
  
 경우는 **암호화** 속성이로 설정 되어 **true** 및 **trustServerCertificate** 속성이 **false** 에서 서버 이름을 지정 하는 경우는 연결 문자열에서 서버 이름과 일치 하지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 인증서를 다음과 같은 오류가 발생 합니다: 드라이버에 보안 연결을 설정할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Secure Sockets Layer (SSL) 암호화를 사용 하 여 합니다. 오류: "java.security.cert.CertificateException: SSL(Secure Sockets Layer)을 초기화하는 동안 인증서의 서버 이름에 대해 유효성 검사를 수행하지 못했습니다."  
  
## <a name="see-also"></a>관련 항목:  
 [SSL 암호화를 사용 하 여](../../connect/jdbc/using-ssl-encryption.md)   
 [JDBC 드라이버 응용 프로그램 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
