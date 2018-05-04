---
title: connect 메서드 (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDriver.connect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43813a4c-1cc7-4659-ba27-f1786f1371eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee87f7694e3612cd89ca3dfa21a691c2aaecb8e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-method-sqlserverdriver"></a>connect 메서드(SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스에 대한 연결을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Connection connect(java.lang.String Url,  
                                   java.util.Properties suppliedProperties)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Url*  
  
 A **문자열** 데이터베이스에 연결 하는 데 사용 되는 URL을 포함 하는 값입니다.  
  
 *suppliedProperties*  
  
 연결 인수로 사용되는 문자열 값 쌍의 집합입니다.  
  
## <a name="return-value"></a>반환 값  
 연결 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 connect 메서드는 java.sql.Driver 인터페이스의 connect 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDriver 메서드](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 멤버](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 클래스](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
