---
title: "setEncrypt 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: setEncrypt Method (SQLServerDataSource)
apilocation: setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e90e49bff2956be8aa6950ec9612ea534921aac
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setencrypt-method-sqlserverdatasource"></a>setEncrypt 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정 된 **부울** encrypt 속성이 사용 되는지 여부를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *암호화*  
  
 **true 이면** 클라이언트 간에 (SECURE Sockets Layer) 암호화가 사용 되는 경우와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>주의  
 Encrypt 속성이로 설정 되어 있으면 **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 서버 인증서가 설치 되어 있으면 클라이언트와 서버 간에 전송 되는 모든 데이터에 대해 SSL 암호화를 사용 합니다. 기본값은 **false**입니다.  
  
 JDBC 드라이버에서는 SSL 핸드셰이크를 설정하려고 할 때 해당 드라이버가 실행 중인 JVM(Java Virtual Machine)을 검색합니다.  
  
 Encrypt 속성이로 설정 되어 있으면 **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] JVM의 기본 JSSE 보안 공급자를 사용 하 여와 SSL 암호화를 협상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다. 기본 보안 공급자는 SSL 암호화를 성공적으로 협상하는 데 필요한 기능을 모두 지원하지 않을 수 있습니다. 예를 들어 기본 보안 공급자에 사용 된 RSA 공개 키의 크기 지원 하지 않을 수 있습니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 인증서입니다. 이 경우 기본 보안 공급자에서 오류가 발생하여 JDBC 드라이버가 연결을 종료합니다. 이 문제를 해결하려면 다음 중 하나를 수행하십시오.  
  
-   구성의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 보다 작은 RSA 공개 키를 가진 서버 인증서와  
  
-   다른 JSSE 보안 공급자를 사용 하도록 JVM을 구성에서 "\<java 홈 > / lib/security/java.security" 보안 속성 파일  
  
-   다른 JVM을 사용합니다.  
  
 Encrypt 속성이 지정 되지 않았거나로 설정 하는 경우 **false**, 드라이버는 적용 하지 않습니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 암호화를 지원 하도록 합니다. 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인스턴스가 SSL 암호화 사용 하도록 구성 되지 않은, 암호화 없이 연결이 설정 됩니다. 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인스턴스가 SSL 암호화를 사용 하도록 구성 되어는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 자동으로 SSL 암호화를 사용 때 구성 된 JVM을 제대로 실행 연결이 종료 되며 드라이버에서 오류가 발생 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
