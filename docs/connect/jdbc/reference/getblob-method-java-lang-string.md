---
title: "getBlob 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getBlob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fe74b50-9ccd-4973-a93a-6da2c20a4154
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 920664ef12bbd45f312c32ce69b35cd568531240
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getblob-method-javalangstring"></a>getBlob 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정 하 여 Java 프로그래밍 언어에 있는 Blob 개체와 지정된 된 JDBC BLOB 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Blob getBlob(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 Blob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getBlob 메서드는 java.sql.CallableStatement 인터페이스의 getBlob 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getBlob 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

