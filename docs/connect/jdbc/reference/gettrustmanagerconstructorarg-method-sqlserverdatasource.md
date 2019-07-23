---
title: getTrustManagerConstructorArg 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getTrustManagerConstructorArg
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f3af347e41f3ba90b283b56d8cb2c1550b69006
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978588"
---
# <a name="gettrustmanagerconstructorarg-method-sqlserverdatasource"></a>getTrustManagerConstructorArg 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  TrustManagerConstructorArg connection 속성의 문자열 값을 반환 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getTrustManagerConstructorArg()  
```  
  
## <a name="return-value"></a>반환 값  
 TrustManagerConstructorArg connection 속성의 값을 포함 하는 **문자열** 이거나, 값이 설정 되어 있지 않은 경우 null입니다.  
  
## <a name="remarks"></a>Remarks  
 TrustManagerClass 속성이 설정 되지 않은 경우 [getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md) 메서드는 null을 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
