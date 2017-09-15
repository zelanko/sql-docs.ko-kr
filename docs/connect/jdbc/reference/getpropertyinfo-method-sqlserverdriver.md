---
title: "getPropertyInfo 메서드 (SQLServerDriver) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDriver.getPropertyInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b5eaad8a-31ef-44ac-af11-d5caa13ac3e2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 08e0490f891f9423f57067512013d19e81aed68f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
  
 A **문자열** 데이터베이스에 연결 하는 데 사용 되는 URL을 포함 하는 값입니다.  
  
 *정보*  
  
 속성 값 쌍(처음 사용할 때는 null)의 목록입니다.  
  
## <a name="return-value"></a>반환 값  
 DriverPropertyInfo 개체의 배열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getPropertyInfo 메서드는 java.sql.Driver 인터페이스의 getPropertyInfo 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDriver 메서드](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 멤버](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 클래스](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
