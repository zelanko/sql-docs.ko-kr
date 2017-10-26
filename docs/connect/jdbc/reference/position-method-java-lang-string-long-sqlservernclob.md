---
title: "position 메서드 (java.lang.String, long) (SQLServerNClob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 46d4beec-831a-449f-98b6-322a80cc499a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 966804e81244d442911f95c163669e2039d608d1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="position-method-javalangstring-long-sqlservernclob"></a>position 메서드(java.lang.String, long)(SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  검색 되는 문자 위치 지정된 된 부분 문자열 *searchstr* 에 표시는 **NCLOB** 값이 표시 **NClob** 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public long position(java.lang.String searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *searchstr*  
  
 검색할 부분 문자열입니다.  
  
 *시작*  
  
 검색을 시작할 위치이며, 첫 번째 위치는 1입니다.  
  
## <a name="return-value"></a>반환 값  
 부분 문자열이 나타나는 위치이며, 부분 문자열이 없으면 -1입니다. 첫 번째 위치는 1입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 위치 메서드 java.sql.NClob 인터페이스의 위치 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [방법 &#40; 배치 SQLServerNClob &#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [SQLServerNClob 메서드](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 멤버](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 클래스](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

