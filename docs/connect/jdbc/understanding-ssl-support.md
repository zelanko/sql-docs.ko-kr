---
title: "SSL 지원 이해 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82440c6d3ffe0ee0f2c2b9080328c0fed302cb31
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-ssl-support"></a>SSL 지원 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]암호화 및 인스턴스의 응용 프로그램이 요청 하는 경우, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 암호화를 지원 하도록 구성 된는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] SSL 핸드셰이크를 시작 합니다. 핸드셰이크를 통해 서버와 클라이언트에서는 데이터 보호에 사용될 암호화 및 암호화 알고리즘을 협상할 수 있습니다. SSL 핸드셰이크가 완료되면 클라이언트와 서버는 암호화된 데이터를 안전하게 전송할 수 있게 됩니다. SSL 핸드셰이크 중 서버는 공개 키 인증서를 클라이언트로 보냅니다. 공개 키 인증서의 발급자를 CA(인증 기관)라고 합니다. 클라이언트는 인증 기관이 신뢰할 수 있는 기관인지 확인해야 합니다.  
  
 응용 프로그램에 암호화를 요청 하지 않고는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 하도록 강제 하지 것입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 암호화를 지원 하도록 합니다. 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스가 SSL 암호화 사용 하도록 구성 되지 않은, 암호화 없이 연결이 설정 됩니다. 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스가 SSL 암호화를 사용 하도록 구성 됩니다, 드라이버는에서 올바르게 구성 된 가상 컴퓨터 JVM (Java)를 실행 하는 경우에 자동으로 SSL 암호화를 사용 또는 다른 연결이 종료 되 고 드라이버에서 오류가 발생 합니다.  
  
> [!NOTE]  
>  에 전달 된 값 **serverName** 에 대체 SAN (주체 이름) SSL 연결에 대 한 서버 인증서에 성공 하려면 CN (일반 이름) 또는 DNS 이름과 정확히 일치 합니다.  
  
> [!NOTE]  
>  SSL을 구성 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 연결 암호화 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 의 항목을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="remarks"></a>주의  
 SSL 암호화를 사용 하도록 응용 프로그램 수 있도록는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 버전 1.2 릴리스부터 다음 연결 속성이: **암호화**, **trustServerCertificate**, **trustStore**, **trustStorePassword**, 및 **hostNameInCertificate**합니다. 자세한 내용은 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 다음 표에서 요약 방법을 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 버전 가능한 SSL 연결 시나리오에 대해 실행 합니다. 각 시나리오는 서로 다른 SSL 연결 속성 집합을 사용합니다. 표에는 다음과 같은 값이 포함되어 있습니다.  
  
-   **빈**: "속성이 연결 문자열에는 존재 하지 않습니다"  
  
-   **값**: "연결 문자열에 속성이 있는지 및 해당 값이 유효한"  
  
-   **모든**: "중요 하지 않습니다는 연결 문자열에 속성이 있는지 여부나 해당 값이 유효한 지 여부 를"  
  
> [!NOTE]  
>  동일한 동작에 대 한 적용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용자 인증 및 Windows 통합된 인증입니다.  
  
|encrypt|trustServerCertificate|hostNameInCertificate|trustStore|trustStorePassword|동작|  
|-------------|----------------------------|---------------------------|----------------|------------------------|--------------|  
|false 또는 blank|any|any|any|any|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 하도록 강제 하지 것입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 암호화를 지원 하도록 합니다. 서버에 자체 서명된 인증서가 있는 경우 드라이버에서 SSL 인증서 교환을 시작합니다. SSL 인증서의 유효성은 검사되지 않으며 자격 증명(로그인 패킷에 있음)만 암호화됩니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구할 경우 드라이버에서 SSL 인증서 교환을 시작합니다. SSL 인증서의 유효성은 검사되지 않지만 전체 통신은 암호화됩니다.|  
|true|true|any|any|any|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다. 되는 경우는 **trustServerCertificate** 속성이 "true", 드라이버는 SSL 인증서의 유효성을 검사 하지 것입니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|비어 있음|비어 있음|비어 있음|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버 ´ ֲ는 **serverName** 서버 SSL 인증서의 유효성을 검사 하 고 인증서 저장소를 사용 하 여 결정 하기 위해 트러스트 관리자 팩터리의 조회 규칙에 의존 하는 연결 URL에 지정 된 속성입니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|value|비어 있음|비어 있음|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버에 대 한 지정 된 값을 사용 하 여 SSL 인증서의 주체 값 유효성을 검사 합니다는 **hostNameInCertificate** 속성입니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|비어 있음|value|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버 ´ ֲ는 **trustStore** 인증서 trustStore 파일을 찾을 수 속성 값 및 **trustStorePassword** trustStore 파일의 무결성을 확인 하려면 속성 값입니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|비어 있음|비어 있음|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버 ´ ֲ는 **trustStorePassword** 속성 값을 기본 trustStore 파일의 무결성을 확인 합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|비어 있음|value|비어 있음|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버 ´ ֲ는 **trustStore** trustStore 파일의 위치를 조회 하는 속성 값입니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|value|비어 있음|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버 ´ ֲ는 **trustStorePassword** 속성 값을 기본 trustStore 파일의 무결성을 확인 합니다. 드라이버를 사용 하는 또한는 **hostNameInCertificate** 속성 값을 SSL 인증서의 유효성을 검사 합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|value|value|비어 있음|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버 ´ ֲ는 **trustStore** trustStore 파일의 위치를 조회 하는 속성 값입니다. 드라이버를 사용 하는 또한는 **hostNameInCertificate** 속성 값을 SSL 인증서의 유효성을 검사 합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
|true|false 또는 blank|value|value|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와 SSL 암호화를 사용 하는 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br /> 클라이언트에서 SSL 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 SSL 인증서 교환을 시작합니다.<br /><br /> 드라이버 ´ ֲ는 **trustStore** 인증서 trustStore 파일을 찾을 수 속성 값 및 **trustStorePassword** trustStore 파일의 무결성을 확인 하려면 속성 값입니다. 드라이버를 사용 하는 또한는 **hostNameInCertificate** 속성 값을 SSL 인증서의 유효성을 검사 합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.|  
  
 Encrypt 속성이로 설정 되어 있으면 **true**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] JVM의 기본 JSSE 보안 공급자를 사용 하 여와 SSL 암호화를 협상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 기본 보안 공급자는 SSL 암호화를 성공적으로 협상하는 데 필요한 기능을 모두 지원하지 않을 수 있습니다. 예를 들어 기본 보안 공급자에 사용 된 RSA 공개 키의 크기 지원 하지 않을 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 인증서입니다. 이 경우 기본 보안 공급자에서 오류가 발생하여 JDBC 드라이버가 연결을 종료합니다. 이 문제를 해결하려면 다음 중 하나를 수행하십시오.  
  
-   구성의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 보다 작은 RSA 공개 키를 가진 서버 인증서와  
  
-   다른 JSSE 보안 공급자를 사용 하도록 JVM을 구성에서 "\<java 홈 > / lib/security/java.security" 보안 속성 파일  
  
-   다른 JVM을 사용합니다.  
  
## <a name="validating-server-ssl-certificate"></a>서버 SSL 인증서의 유효성 검사  
 SSL 핸드셰이크 중 서버는 공개 키 인증서를 클라이언트로 보냅니다. JDBC 드라이버 또는 클라이언트는 클라이언트에서 신뢰하는 인증 기관에서 서버 인증서를 발행했는지 검사해야 합니다. 서버 인증서는 다음 조건을 충족해야 합니다.  
  
-   인증서가 신뢰할 수 있는 인증 기관에 의해 발행되었습니다.  
  
-   인증서는 서버 인증용으로 발행되어야 합니다.  
  
-   인증서가 만료되지 않았습니다.  
  
-   CN (일반 이름) 주체에서 또는 DNS 이름에는 대체 SAN (주체 이름) 인증서의 정확히 일치 하는 **serverName** 연결 문자열에 지정 된 값을 지정 하는 경우는  **hostNameInCertificate** 속성 값입니다.  
  
-   DNS 이름은 와일드카드 문자를 포함할 수 있습니다. 하지만 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 와일드 카드 일치를 지원 하지 않습니다. 즉, abc.com *.com 일치 하지 것입니다 되지만 \*.com 일치시킬지 \*. com입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SSL 암호화를 사용 하 여](../../connect/jdbc/using-ssl-encryption.md)   
 [JDBC 드라이버 응용 프로그램 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  

