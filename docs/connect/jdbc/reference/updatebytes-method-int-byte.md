---
title: updateBytes 메서드 (int, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes (int, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 625f48ba-53d0-45a6-8fcb-643f1e0cbe8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60de0b0fd051ed67a2f2804443e419d454c2cb5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996910"
---
# <a name="updatebytes-method-int-byte"></a>updateBytes 메서드(int, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 인덱스가 지정된 경우 지정된 열을 **byte** 값의 배열로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBytes(int index,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 **바이트** 값의 배열입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateBytes 메서드는 java.sql.ResultSet 인터페이스의 updateBytes 메서드에 의해 지정됩니다.  
  
 이전 버전의 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 SQLServerResultSet.updateBytes를 사용하여 바이트 배열과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 **date**, **time**, **datetime2** 또는 **datetimeoffset** 간에 값을 변환할 수 있었습니다. 이제 이 메서드와 이러한 데이터 형식을 함께 사용하면 변환이 지원되지 않음을 나타내는 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBytes 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
