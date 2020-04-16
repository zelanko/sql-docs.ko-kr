---
title: 애플리케이션 보안 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f7d9c9a1610b5ebcd086bec1cc11d0ec85f7358
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219442"
---
# <a name="application-security"></a>애플리케이션 보안
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용할 때는 애플리케이션의 보안을 확보하기 위해 미리 주의를 기울여야 합니다. 다음 섹션에서는 애플리케이션의 보안을 확보하기 위해 수행할 수 있는 단계에 관한 정보를 제공합니다.  
  
## <a name="using-java-policy-permissions"></a>Java 정책 권한 사용  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용할 때는 JDBC 드라이버에서 요구하는 필수 Java 정책 권한을 지정해야 합니다. JRE(Java Runtime Environment)는 런타임에 사용하여 스레드가 리소스에 액세스할 수 있는지 여부를 확인할 수 있는 다양한 보안 모델을 제공합니다. 이러한 액세스는 보안 정책 파일을 통해 제어할 수 있습니다. 또한 이 정책 파일은 배포자와 컨테이너의 sysadmin을 통해 관리되지만 이 항목에 나열된 권한은 JDBC 드라이버의 기능에 영향을 주는 권한입니다.  
  
 정책 파일의 일반적인 권한은 다음과 같습니다.  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 다음 코드베이스는 최소한의 권한을 부여하도록 JDBC 드라이버 코드베이스로 제한해야 합니다.  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  "file:/install_dir/lib/-" 코드는 JDBC 드라이버의 설치 디렉터리를 나타냅니다.  
  
## <a name="protecting-server-communication"></a>서버 통신 보호  
 JDBC 드라이버를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 통신하는 경우, IPSEC(인터넷 프로토콜 보안), 이전에 SSL(Secure Sockets Layer)로 알려진 TLS(전송 계층 보안) 또는 둘 다를 사용하여 통신 채널의 보안을 유지할 수 있습니다.  
  
 TLS 지원을 사용하여 IPSec 외에 추가 수준의 보호 기능을 제공할 수 있습니다. TLS를 사용하는 방법에 대한 자세한 내용은 [암호화 사용](../../connect/jdbc/using-ssl-encryption.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 애플리케이션 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
