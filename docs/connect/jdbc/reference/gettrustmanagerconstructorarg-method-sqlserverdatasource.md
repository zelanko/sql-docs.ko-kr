---
description: getTrustManagerConstructorArg 메서드(SQLServerDataSource)
title: getTrustManagerConstructorArg 메서드(SQLServerDataSource) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: edda767e361b540833babd0125f3f13ad5f2fb08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433975"
---
# <a name="gettrustmanagerconstructorarg-method-sqlserverdatasource"></a>getTrustManagerConstructorArg 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  TrustManagerConstructorArg 연결 속성의 문자열 값을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getTrustManagerConstructorArg()  
```  
  
## <a name="return-value"></a>Return Value  
 TrustManagerConstructorArg 연결 속성의 값을 포함하는 **문자열**입니다. 값이 설정되어 있지 않은 경우에는 Null입니다.  
  
## <a name="remarks"></a>설명  
 TrustManagerClass 속성이 설정되어 있지 않은 경우 [getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md) 메서드는 Null을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
