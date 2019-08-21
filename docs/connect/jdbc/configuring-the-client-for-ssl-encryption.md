---
title: SSL 암호화를 위한 클라이언트 구성 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50c1a24dfbfb925cbda961f8a566e0d1bcd26bdf
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028200"
---
# <a name="configuring-the-client-for-ssl-encryption"></a>SSL 암호화에 대한 클라이언트 구성
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 또는 클라이언트는 서버가 올바른 서버이며 서버 인증서가 클라이언트에서 신뢰하는 인증 기관에서 발행되었는지 유효성을 검사해야 합니다. 서버 인증서의 유효성을 검사하기 위해서는 연결 시 트러스트 자료를 제공해야 합니다. 또한 서버 인증서의 발급자가 클라이언트에서 신뢰하는 인증 기관이어야 합니다.  
  
 이 항목에서는 먼저 클라이언트 컴퓨터에 트러스트 자료를 제공하는 방법에 대해 설명합니다. 그런 다음 SQL Server 인스턴스의 SSL(Secure Sockets Layer) 인증서가 프라이빗 인증 기관에서 발행된 경우 서버 인증서를 클라이언트 컴퓨터의 트러스트 저장소로 가져오는 방법에 대해 설명합니다.  
  
 서버 인증서의 유효성을 검사하는 방법은 [SSL 지원 이해](../../connect/jdbc/understanding-ssl-support.md)의 서버 SSL 인증서 유효성 검사 섹션을 참조하세요.  
  
## <a name="configuring-the-client-trust-store"></a>클라이언트 트러스트 저장소 구성 
 서버 인증서의 유효성을 검사하려면 명시적으로 **trustStore** 및 **trustStorePassword** 연결 속성을 사용하거나 암시적으로 기본 JVM(Java Virtual Machine)의 기본 트러스트 저장소를 사용하여 연결 시에 트러스트 자료를 제공해야 합니다. 연결 문자열에 **trustStore** 및 **trustStorePassword** 속성을 설정하는 방법은 [SSL 암호화를 사용해 연결](../../connect/jdbc/connecting-with-ssl-encryption.md)을 참조하세요.  
  
 **trustStore** 속성이 지정되지 않았거나 null로 설정된 경우 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 기본 JVM의 보안 공급자인 Java Secure Socket Extension(SunJSSE)을 사용합니다. SunJSSE 공급자는 기본 TrustManager를 제공하는데 이 속성은 트러스트 저장소에 제공된 트러스트 자료에 대해 SQL Server에서 반환한 X.509 인증서의 유효성을 검사하는 데 사용됩니다.  
  
 TrustManager는 다음 검색 순서에 따라 기본 trustStore를 찾으려고 합니다.  
  
-   시스템 속성 “javax.net.ssl.trustStore”가 정의된 경우 TrustManager는 해당 시스템 속성에 지정된 파일 이름을 사용하여 기본 trustStore 파일을 찾으려고 합니다.  
  
-   “javax.net.ssl.trustStore” 시스템 속성이 정의되지 않은 경우와 “\<java-home>/lib/security/jssecacerts” 파일이 있는 경우 해당 파일이 사용됩니다.  
  
-   “\<java-home>/lib/security/cacerts” 파일이 있는 경우 해당 파일이 사용됩니다.  
  
 자세한 내용은 Sun Microsystems 웹 사이트에서 SUNX509 TrustManager 인터페이스 설명서를 참조하십시오.  
  
 Java Runtime Environment를 사용하면 trustStore 및 trustStorePassword 시스템 속성을 다음과 같이 설정할 수 있습니다.  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 이 경우 이 JVM에서 실행 중인 모든 애플리케이션이 이러한 설정을 기본값으로 사용합니다. 애플리케이션에서 기본 설정을 재정의하려면 연결 문자열 또는 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스의 해당 setter 메서드에서 **trustStore** 및 **trustStorePassword** 연결 속성을 설정해야 합니다.  
  
 또한 “\<java-home>/lib/security/jssecacerts” 및 “\<java-home>/lib/security/cacerts”와 같은 기본 트러스트 저장소 파일을 구성하고 관리할 수도 있습니다. 이를 위해서는 JRE(Java Runtime Environment)와 함께 설치되는 JAVA "keytool" 유틸리티를 사용하십시오. "keytool" 유틸리티에 대한 자세한 내용은 Sun Microsystems 웹 사이트에서 keytool 설명서를 참조하십시오.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>트러스트 저장소로 서버 인증서 가져오기  
 SSL 핸드셰이크 중 서버에서는 공개 키 인증서를 클라이언트로 보내는데 공개 키 인증서의 발급자를 CA(인증 기관)라고 합니다. 클라이언트에서는 인증 기관이 신뢰할 수 있는 기관인지 확인해야 합니다. 신뢰할 수 있는 CA의 공개 키를 알고 있으면 이를 확인할 수 있습니다. 일반적으로 JVM은 미리 정의된 신뢰할 수 있는 인증 기관 집합과 함께 제공됩니다.  
  
 SQL Server 인스턴스의 SSL 인증서가 프라이빗 인증 기관에서 발행된 경우 클라이언트 컴퓨터의 트러스트 저장소에 있는 신뢰할 수 있는 인증서 목록에 해당 인증 기관의 인증서를 추가해야 합니다.  
  
 이를 위해서는 JRE(Java Runtime Environment)와 함께 설치되는 JAVA "keytool" 유틸리티를 사용하십시오. 다음 명령 프롬프트는 "keytool" 유틸리티를 사용하여 파일에서 인증서를 가져오는 방법을 보여 줍니다.  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 이 예에서는 "caCert.cer" 파일을 인증서 파일로 사용합니다. 이 인증서 파일은 서버에서 가져와야 합니다. 다음은 서버 인증서를 파일로 내보내는 방법을 설명하는 단계입니다.  
  
1.  시작, 실행을 차례로 클릭하고 MMC를 입력합니다. MMC는 Microsoft Management Console의 머리 글자어입니다.  
  
2.  MMC에서 인증서를 엽니다.  
  
3.  개인, 인증서를 차례로 확장합니다.  
  
4.  서버 인증서를 마우스 오른쪽 단추로 클릭한 다음 모든 작업/내보내기를 선택합니다.  
  
5.  다음을 클릭하여 인증서 내보내기 마법사의 시작 대화 상자에서 이동합니다.  
  
6.  "아니요, 프라이빗 키를 내보내지 않습니다."가 선택되어 있는지 확인하고 다음을 클릭합니다.  
  
7.  DER 인코딩 이진 X.509(.CER) 또는 Base-64 인코딩 X.509(.CER)가 선택되어 있는지 확인하고 다음을 클릭합니다.  
  
8.  내보낼 파일 이름을 입력합니다.  
  
9. 다음을 클릭한 다음 마침을 클릭하여 인증서를 내보냅니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SSL 암호화 사용](../../connect/jdbc/using-ssl-encryption.md)   
 [JDBC 드라이버 애플리케이션 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
