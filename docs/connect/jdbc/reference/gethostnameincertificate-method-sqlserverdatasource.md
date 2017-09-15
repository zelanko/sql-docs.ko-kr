---
title: "getHostNameInCertificate 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d74305f9c389da375a26bf0516f577939b50f7e9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>getHostNameInCertificate 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL Server SSL(Secure Sockets Layer) 인증서의 유효성을 검사하는 데 사용되는 호스트 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 호스트 이름 또는 값 설정 하지 않으면 null이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 호스트 이름은 통신 계층이 SSL을 사용하여 암호화된 경우 SQL Server SSL 인증서 값의 유효성을 검사하는 데 사용됩니다.  
  
 호스트 이름 설정 하지 않으면는 [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) 메서드가 null을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
