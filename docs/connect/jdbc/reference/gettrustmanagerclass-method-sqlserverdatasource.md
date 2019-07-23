---
title: getTrustManagerClass 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getTrustManagerClass
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 567f5e7e3aca87b875e4f93c26d7caa5535a8c75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978607"
---
# <a name="gettrustmanagerclass-method-sqlserverdatasource"></a>getTrustManagerClass 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  TrustManagerClass 연결 속성의 문자열 값을 반환 합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getTrustManagerClass()  
```  
  
## <a name="return-value"></a>반환 값  
 TrustManagerClass 연결 속성의 값을 포함 하는 **문자열** 이거나, 값이 설정 되어 있지 않은 경우 null입니다.  
  
## <a name="remarks"></a>Remarks  
 TrustManagerClass 속성이 설정 되지 않은 경우 [Gettrustmanagerclass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md) 메서드는 null을 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
