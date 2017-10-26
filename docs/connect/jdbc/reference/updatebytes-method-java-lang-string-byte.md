---
title: "updateBytes 메서드 (java.lang.String, byte) | Microsoft Docs"
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
- SQLServerResultSet.updateBytes (java.lang.String, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fb9de2b-61bc-4c96-89a5-c07cd7ee201a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 995ae6ccb99dcf1b982d4675697ca7e4953487a0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatebytes-method-javalangstring-byte"></a>updateBytes 메서드 (java.lang.String, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 열을의 배열로 업데이트 **바이트** 열 이름이 지정 된 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBytes(java.lang.String columnName,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
 *x*  
  
 배열을 **바이트** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateBytes 메서드는 java.sql.ResultSet 인터페이스의 updateBytes 메서드에 의해 지정 됩니다.  
  
 이전 버전의에서 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], SQLServerResultSet.updateBytes를 사용 하 여 바이트 배열 간에 값을 변환할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식 **날짜**, **시간**, ** datetime2**, 또는 **datetimeoffset**합니다. 이제 이 메서드와 이러한 데이터 형식을 함께 사용하면 변환이 지원되지 않음을 나타내는 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateBytes 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

