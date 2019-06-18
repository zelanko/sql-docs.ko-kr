---
title: absolute 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b0572ed756bd8b347c01e05168873ac543a0ea7e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66783563"
---
# <a name="absolute-method-sqlserverresultset"></a>absolute 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서를 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 지정된 행으로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *행*  
  
 이동할 행 번호를 나타내는 **int**입니다. 양수, 음수 또는 0일 수 있습니다.  
  
## <a name="return-value"></a>반환 값  
 커서가 지정된 위치로 이동하는 경우 **true**입니다. 첫 번째 행 앞이나 마지막 행 뒤로 이동하는 경우 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 absolute 메서드는 java.sql.ResultSet 인터페이스의 absolute 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
