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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 248213fed555ffc029162c44bdcccb656c311703
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974292"
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
  
 클라이언트와 **간에 SSL(Secure Sockets Layer) 암호화가 사용되면**true[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 encrypt 속성이 **true**로 설정되어 있으면 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 서버에 인증서가 설치되어 있는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 클라이언트와 서버 간에 전송되는 모든 데이터에 대해 SSL 암호화를 사용하도록 지정합니다. 기본 값은 **false**입니다.  
  
 JDBC 드라이버에서는 SSL 핸드셰이크를 설정하려고 할 때 해당 드라이버가 실행 중인 JVM(Java Virtual Machine)을 검색합니다.  
  
 encrypt 속성이 **true**로 설정되어 있는 경우 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 JVM의 기본 JSSE 보안 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 SSL 암호화를 협상합니다. 기본 보안 공급자는 SSL 암호화를 성공적으로 협상하는 데 필요한 기능을 모두 지원하지 않을 수 있습니다. 예를 들어 기본 보안 공급자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 인증서에 사용되는 RSA 공개 키의 크기를 지원하지 않을 수 있습니다. 이 경우 기본 보안 공급자에서 오류가 발생하여 JDBC 드라이버가 연결을 종료합니다. 이 문제를 해결하려면 다음 중 하나를 수행하십시오.  
  
-   보다 작은 RSA 공개 키를 사용하는 서버 인증서로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성  
  
-   "\<java-home>/lib/security/java.security" 보안 속성 파일에서 다른 JSSE 보안 공급자를 사용하도록 JVM 구성  
  
-   다른 JVM을 사용합니다.  
  
 encrypt 속성이 지정되어 있지 않거나 **false**로 설정되어 있으면 드라이버에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 SSL 암호화를 지원하도록 지정하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 SSL 암호화를 사용하도록 구성되어 있지 않으면 암호화 없이 연결이 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 SSL 암호화를 사용하도록 구성되어 있으면 올바르게 구성된 JVM에서 실행될 때 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 자동으로 SSL 암호화를 사용하고, 그렇지 않은 경우 연결이 종료되며 드라이버에서 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
