---
title: 암호화 지원 이해 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ec3ad142e3dc5e2945afebeb2c9a6c97350672c
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713304"
---
# <a name="understanding-encryption-support"></a>암호화 지원 이해

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

애플리케이션에서 암호화를 요청하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스가 TLS 암호화를 지원하도록 구성되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 TLS 핸드셰이크를 시작합니다. 핸드셰이크를 통해 서버와 클라이언트에서는 데이터 보호에 사용될 암호화 및 암호화 알고리즘을 협상할 수 있습니다. TLS 핸드셰이크가 완료되면 클라이언트와 서버는 암호화된 데이터를 안전하게 전송할 수 있게 됩니다. TLS 핸드셰이크 중 서버에서는 공개 키 인증서를 클라이언트로 보내는데 공개 키 인증서의 발급자를 CA(인증 기관)라고 합니다. 클라이언트는 인증 기관이 신뢰할 수 있는 기관인지 확인해야 합니다.  
  
애플리케이션에서 암호화를 요청하지 않는 경우 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 TLS 암호화를 지원하도록 적용하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 TLS 암호화를 사용하도록 구성되어 있지 않으면 암호화 없이 연결이 설정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 TLS 암호화를 사용하도록 구성되어 있으면 올바르게 구성된 JVM(Java Virtual Machine)에서 실행될 때 드라이버는 자동으로 TLS 암호화를 사용하고, 그렇지 않으면 연결이 종료되며 드라이버에서 오류가 발생합니다.  
  
> [!NOTE]  
> TLS 연결이 성공하려면 **serverName**에 전달된 값이 서버 인증서의 SAN(주체 대체 이름)에 있는 CN(일반 이름) 또는 DNS 이름과 정확히 일치하는지 확인합니다.  
>
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 TLS를 구성 하는 방법에 대 한 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조 하세요.  
  
## <a name="remarks"></a>Remarks

애플리케이션에서 TLS 암호화를 사용할 수 있도록 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 버전 1.2 릴리스부터 **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword**, **hostNameInCertificate** 등의 연결 속성이 제공됩니다. 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
 다음 표에는 가능한 TLS 연결 시나리오에 대해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 버전이 어떻게 동작하는지 요약되어 있습니다. 각 시나리오는 서로 다른 TLS 연결 속성 집합을 사용합니다. 표에는 다음과 같은 값이 포함되어 있습니다.  
  
- **blank**: "연결 문자열에 속성이 없습니다."  
  
- **value**: "연결 문자열에 속성이 있으며 해당 값이 유효합니다."  
  
- **any**: "연결 문자열에 속성이 있는지 여부나 해당 값이 유효한지 여부가 중요하지 않습니다."  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 인증 및 Windows 통합 인증에 대해서도 같은 동작이 적용됩니다.  
  
| encrypt        | trustServerCertificate | hostNameInCertificate | trustStore | trustStorePassword | 동작                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ---------------------- | --------------------- | ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| false 또는 blank | any                    | any                   | any        | any                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 지원하도록 적용하지 않습니다. 서버에 자체 서명된 인증서가 있는 경우 드라이버에서 TLS 인증서 교환을 시작합니다. TLS 인증서의 유효성은 검사되지 않으며 자격 증명(로그인 패킷에 있음)만 암호화됩니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구할 경우 드라이버에서 TLS 인증서 교환을 시작합니다. TLS 인증서의 유효성은 검사되지 않지만 전체 통신은 암호화됩니다.                                                                                                                                                                                    |
| true           | true                   | any                   | any        | any                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다. **trustServerCertificate** 속성이 "true"로 설정되어 있는 경우 드라이버에서 TLS 인증서의 유효성을 검사하지 않습니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                                                                                                                                          |
| true           | false 또는 blank         | 비어 있음                 | 비어 있음      | 비어 있음              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 연결 URL에 지정된 **serverName** 속성을 사용하여 서버 TLS 인증서의 유효성을 검사하며 트러스트 관리자 팩터리의 조회 규칙에 따라 사용할 인증서 저장소를 결정합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                             |
| true           | false 또는 blank         | value                 | 비어 있음      | 비어 있음              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 **hostNameInCertificate** 속성에 대해 지정된 값을 사용하여 TLS 인증서 주체 값의 유효성을 검사합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                                                                                                                 |
| true           | false 또는 blank         | 비어 있음                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 **trustStore** 속성 값을 사용하여 인증서 trustStore 파일을 찾고 **trustStorePassword** 속성 값을 사용하여 trustStore 파일의 무결성을 검사합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                                                                |
| true           | false 또는 blank         | 비어 있음                 | 비어 있음      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 **trustStorePassword** 속성 값을 사용하여 기본 trustStore 파일의 무결성을 검사합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                                                                                                                                  |
| true           | false 또는 blank         | 비어 있음                 | value      | 비어 있음              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 **trustStore** 속성 값을 사용하여 trustStore 파일의 위치를 조회합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                                                                                                                                                 |
| true           | false 또는 blank         | value                 | 비어 있음      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 **trustStorePassword** 속성 값을 사용하여 기본 trustStore 파일의 무결성을 검사합니다. 또한 **hostNameInCertificate** 속성 값을 사용하여 TLS 인증서의 유효성을 검사합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                   |
| true           | false 또는 blank         | value                 | value      | 비어 있음              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 **trustStore** 속성 값을 사용하여 trustStore 파일의 위치를 조회합니다. 또한 **hostNameInCertificate** 속성 값을 사용하여 TLS 인증서의 유효성을 검사합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다.                                                                                  |
| true           | false 또는 blank         | value                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 암호화를 사용하도록 요청합니다.<br /><br /> 클라이언트에서 TLS 암호화를 지원하도록 서버가 요구하거나 서버에서 암호화를 지원하는 경우 드라이버에서 TLS 인증서 교환을 시작합니다.<br /><br /> 드라이버는 **trustStore** 속성 값을 사용하여 인증서 trustStore 파일을 찾고 **trustStorePassword** 속성 값을 사용하여 trustStore 파일의 무결성을 검사합니다. 또한 **hostNameInCertificate** 속성 값을 사용하여 TLS 인증서의 유효성을 검사합니다.<br /><br /> 서버가 암호화를 지원하도록 구성되어 있지 않은 경우 드라이버에서 오류가 발생하고 연결이 종료됩니다. |
  
encrypt 속성이 **true**로 설정되어 있는 경우 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 JVM의 기본 JSSE 보안 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 TLS 암호화를 협상합니다. 기본 보안 공급자는 TLS 암호화를 성공적으로 협상하는 데 필요한 기능을 모두 지원하지 않을 수 있습니다. 예를 들어 기본 보안 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TLS 인증서에 사용되는 RSA 공개 키의 크기를 지원하지 않을 수 있습니다. 이 경우 기본 보안 공급자에서 오류가 발생하여 JDBC 드라이버가 연결을 종료합니다. 이 문제를 해결하려면 다음 중 하나를 수행하십시오.  
  
- 보다 작은 RSA 공개 키를 사용하는 서버 인증서로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성  
  
- "\<java-home>/lib/security/java.security" 보안 속성 파일에서 다른 JSSE 보안 공급자를 사용하도록 JVM 구성  
  
- 다른 JVM을 사용합니다.  
  
## <a name="validating-server-tls-certificate"></a>서버 TLS 인증서 유효성 검사  

TLS 핸드셰이크 중 서버에서는 공개 키 인증서를 클라이언트로 보내는데 JDBC 드라이버 또는 클라이언트는 클라이언트에서 신뢰하는 인증 기관에서 서버 인증서를 발행했는지 검사해야 합니다. 서버 인증서는 다음 조건을 충족해야 합니다.  
  
- 인증서가 신뢰할 수 있는 인증 기관에 의해 발행되었습니다.  
  
- 인증서는 서버 인증용으로 발행되어야 합니다.  
  
- 인증서가 만료되지 않았습니다.  
  
- 주체의 CN(일반 이름) 또는 인증서의 SAN(주체 대체 이름)에 있는 DNS 이름은 연결 문자열 또는 **hostNameInCertificate** 속성 값(지정된 경우)에 지정된 **serverName** 값과 정확히 일치합니다.  
  
- DNS 이름은 와일드카드 문자를 포함할 수 있습니다. 그러나 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 와일드카드 일치를 지원하지 않습니다. 즉, abc.com은 \*.com과 일치하지 않지만 \*.com은 \*.com과 일치합니다.  
  
## <a name="see-also"></a>관련 항목:

[암호화 사용](../../connect/jdbc/using-ssl-encryption.md)

[JDBC 드라이버 애플리케이션 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
