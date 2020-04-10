---
title: setAuthenticationScheme(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b942f78e-7ce1-44ef-923d-a7c3d7c76b83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08d9483a97be92acf7b08104e2f285fb954673ed
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924475"
---
# <a name="setauthenticationscheme-sqlserverdatasource"></a>setAuthenticationScheme(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  애플리케이션에서 사용하려는 통합 보안의 종류를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
public void setAuthenticationScheme(String authenticationScheme);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *authenticationScheme*  
  
 값은 **“JavaKerberos”** 및 기본값 **“NativeAuthentication”** 입니다. 자세한 내용은 [Kerberos 통합 인증을 사용하여 SQL Server에 연결](../../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
