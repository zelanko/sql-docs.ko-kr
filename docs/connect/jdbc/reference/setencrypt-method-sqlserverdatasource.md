---
title: setEncrypt 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da0aa987f1ec773e2f61e738bc4045136c64859a
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219242"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>setEncrypt 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  encrypt 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *encrypt*  
  
 이전에 SSL(Secure Sockets Layer)로 알려진 TLS(전송 계층 보안) 암호화를 클라이언트와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 간에 사용하도록 설정한 경우 **true**입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 encrypt 속성이 **true**로 설정되어 있으면, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 서버에 인증서가 설치된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 클라이언트와 서버 간에 전송되는 모든 데이터에 대해 TLS 암호화를 사용하도록 지정합니다. 기본 값은 **false**입니다.  
  
 JDBC 드라이버는 TLS 핸드셰이크를 설정할 때 드라이버를 실행 중인 JVM(Java Virtual Machine)을 검색합니다.  
  
 encrypt 속성이 **true**로 설정되어 있는 경우 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 JVM의 기본 JSSE 보안 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 TLS 암호화를 협상합니다. 기본 보안 공급자는 TLS 암호화를 성공적으로 협상하는 데 필요한 기능을 모두 지원하지 않을 수 있습니다. 예를 들어 기본 보안 공급자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 인증서에 사용되는 RSA 퍼블릭 키의 크기를 지원하지 않을 수 있습니다. 이 경우 기본 보안 공급자에서 오류가 발생하여 JDBC 드라이버가 연결을 종료합니다. 이 문제를 해결하려면 다음 중 하나를 수행하십시오.  
  
-   보다 작은 RSA 공개 키를 사용하는 서버 인증서로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성  
  
-   "\<java-home>/lib/security/java.security" 보안 속성 파일에서 다른 JSSE 보안 공급자를 사용하도록 JVM 구성  
  
-   다른 JVM을 사용합니다.  
  
 encrypt 속성이 지정되어 있지 않거나 **false**로 설정되어 있으면, 드라이버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 TLS 암호화를 지원하도록 적용하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 강제로 TLS 암호화를 사용하도록 구성되어 있지 않으면 암호화 없이 연결이 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 TLS 암호화를 사용하도록 구성되어 있으면, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 올바르게 구성된 JVM에서 실행 중인 경우 자동으로 TLS 암호화를 사용합니다. 그렇지 않으면 연결이 종료되고 드라이버에서 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
