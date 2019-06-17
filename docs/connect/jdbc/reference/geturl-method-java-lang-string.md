---
title: getURL 메서드 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getURL (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb709f6b-64e1-4d0c-a704-290891627dd7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: add077cc98e9453b5523c816ff9c47b67a13272c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779823"
---
# <a name="geturl-method-javalangstring"></a>getURL 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 Java 프로그래밍 언어의 URL 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.net.URL getURL(java.lang.String s)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *s*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 URL 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getURL 메서드는 java.sql.CallableStatement 인터페이스의 getURL 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getURL 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
