---
title: setTrustServerCertificate 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea37bbfb1582836db8f0c12b383b59c2d527f5ef
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219229"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustServerCertificate 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *trustServerCertificate*  
  
 통신 계층이 TLS를 사용하여 암호화된 경우 이전에 SSL(Secure Sockets Layer)로 알려진 서버 TLS(전송 계층 보안) 인증서를 자동으로 신뢰해야 하면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="remarks"></a>설명  
 trustServerCertificate 속성이 **true**로 설정되어 있으면, 통신 계층이 TLS를 사용하여 암호화된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 인증서가 자동으로 신뢰됩니다. 즉, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 인증서의 유효성을 검사하지 않습니다. 기본 값은 **false**입니다.  
  
 trustServerCertificate 속성이 **false**로 설정되어 있으면, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서 서버 TLS/SSL 인증서의 유효성을 검사합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
