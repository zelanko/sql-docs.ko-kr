---
title: getHostNameInCertificate 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 67978d2597a5167d3930c85ee453dc6d985f021e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982905"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>getHostNameInCertificate 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQL Server SSL(Secure Sockets Layer) 인증서의 유효성을 검사하는 데 사용되는 호스트 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>반환 값  
 호스트 이름이 들어 있는 **String**이며, 값이 설정되어 있지 않은 경우 null입니다.  
  
## <a name="remarks"></a>Remarks  
 호스트 이름은 통신 계층이 SSL을 사용하여 암호화된 경우 SQL Server SSL 인증서 값의 유효성을 검사하는 데 사용됩니다.  
  
 호스트 이름이 설정되어 있지 않으면 [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) 메서드는 null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
