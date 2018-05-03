---
title: getFloat 메서드 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getFloat (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 40178471-4f35-4df9-b3fb-80cdf43de274
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18d13d3f86f1273f30456ba67f3c6f59c7731e07
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getfloat-method-int"></a>getFloat 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  로 지정된 된 매개 변수의 값을 검색 하는 **float** java 프로그래밍 언어 매개 변수 인덱스가 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public float getFloat(int index)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱스*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **float** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getFloat 메서드는 java.sql.CallableStatement 인터페이스의 getFloat 메서드에 의해 지정 됩니다.  
  
 이 메서드는 Java 모든 숫자 기반 형식을 반환 **float** 충실도 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getFloat 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
