---
title: setAuthenticationScheme (SQLServerDataSource) | Microsoft Docs
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
ms.assetid: b942f78e-7ce1-44ef-923d-a7c3d7c76b83
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 769db93f9bc1e0609ebbebcadf2fdd6f3cda3b4c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setauthenticationscheme-sqlserverdatasource"></a>setAuthenticationScheme(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응용 프로그램에서 사용하려는 통합 보안의 종류를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
public void setAuthenticationScheme(String authenticationScheme);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *authenticationScheme*  
  
 값은 **"JavaKerberos"** 및 기본 **"NativeAuthentication"**합니다. 자세한 내용은 참조 [Kerberos 통합 인증을 사용 하려면 SQL Server에 연결](../../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
