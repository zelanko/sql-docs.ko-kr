---
title: "getSQLXML 메서드 (int) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a1b32d3a-d7c9-4086-ae2b-fc1da96949b1
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8feded5f078b0a6202ef39a0c0e5939fa2debd6f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getsqlxml-method-int"></a>getSQLXML 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정 된 SQLXML 개체와 지정된 된 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.SQLXML getSQLXML(int parameterIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 ASQLXMLobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSQLXML 메서드는 java.sql.CallableStatement 인터페이스의 getSQLXML 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getSQLXML 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
