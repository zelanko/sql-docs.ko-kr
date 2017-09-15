---
title: "setClob 메서드 (java.lang.String, java.io.Reader, long) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bc9fddea-134e-4440-ba54-a1f74bb40c46
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 431e5d0c93de8a18206312bd4f40082b12d2305b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setclob-method-javalangstring-javaioreader-long"></a>setClob 메서드(java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 문자 길이의 지정 된 판독기 개체에 지정된 된 매개 변수를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setClob(java.lang.String parameterName,  
            java.io.Reader value,  
            long length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *value*  
  
 판독기 개체입니다.  
  
 *length*  
  
 A **긴** 스트림의 문자 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setClob 메서드는 java.sql.CallableStatement 인터페이스의 setClob 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setClob 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
