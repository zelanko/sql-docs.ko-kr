---
title: "getBlob 메서드 (int) | Microsoft Docs"
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
- SQLServerCallableStatement.getBlob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bef3ef12-cdda-4a18-90d6-4a501b8e30f0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7de04a59b86448deabf7d2ffb3bcfa0668e699ab
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getblob-method-int"></a>getBlob 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정 하 여 Java 프로그래밍 언어에 있는 Blob 개체와 지정된 된 JDBC BLOB 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Blob getBlob(int index)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱스*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
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
  
  

