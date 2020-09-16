---
description: getPropertyInfo 메서드(SQLServerDriver)
title: getPropertyInfo 메서드(SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.getPropertyInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b5eaad8a-31ef-44ac-af11-d5caa13ac3e2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cfdcc8917d818ff74d5897e9481f829f1284bdee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434925"
---
# <a name="getpropertyinfo-method-sqlserverdriver"></a>getPropertyInfo 메서드(SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스에 연결하기 위해 필요한 속성을 검색하는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.DriverPropertyInfo[] getPropertyInfo(java.lang.String Url,  
                                                     java.util.Properties Info)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Url*  
  
 데이터베이스에 연결하는 데 사용되는 URL이 들어 있는 **String** 값입니다.  
  
 *정보*  
  
 속성 값 쌍(처음 사용할 때는 null)의 목록입니다.  
  
## <a name="return-value"></a>반환 값  
 DriverPropertyInfo 개체의 배열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getPropertyInfo 메서드는 java.sql.Driver 인터페이스의 getPropertyInfo 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDriver 메서드](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 멤버](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 클래스](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
