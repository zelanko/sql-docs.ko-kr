---
title: "getNString 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c6a228bf0087d5af7b5f44ce2888b29d9ed73351
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getnstring-method-javalangstring"></a>getNString 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 값을 검색 **NCHAR**, **NVARCHAR**, 또는 **LONGNVARCHAR** java에서 프로그래밍 언어 문자열 매개 변수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 AStringobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getNString 메서드는 java.sql.CallableStatement 인터페이스의 getNString 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getNString 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 메서드](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  
