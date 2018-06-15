---
title: setHostNameInCertificate 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 774f2cd158612f0029212014e53e380cef180c04
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32842918"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  유효성을 검사 하는 데 사용할 호스트 이름을 설정 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] (SECURE Sockets Layer) 인증서입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *hostNameInCertificate*  
  
 A **문자열** 호스트 이름이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 HostNameInCertificate 값 확인을 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 통신 계층이 SSL을 사용 하 여 암호화 된 경우 SSL 인증서입니다. 기본값은 null입니다.  
  
 HostNameInCertificate 속성은 null로 설정 되었거나 지정 되지 않은 경우는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] serverName 속성 값을 사용 하 여 유효성을 검사할 됩니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL 인증서입니다. hostNameInCertificate 속성이 문자열이나 빈 문자열 ""로 설정된 경우 드라이버에서는 해당 값을 사용하여 서버 SSL 인증서의 유효성을 검사합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
