---
title: "getBigDecimal 메서드 (int, int) (SQLServerResultSet) | Microsoft Docs"
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
apiname: SQLServerResultSet.getBigDecimal (int, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: c99d0772-b26c-492c-a643-2813b5429993
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e846c83b1603bca2d0055a85b1958af2601bfff
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getbigdecimal-method-int-int-sqlserverresultset"></a>getBigDecimal 메서드 (int, int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 지정 된 소수 자릿수를 사용 하 여 개체입니다.  
  
> [!NOTE]  
>  이 메서드는 JDBC 사양에서 더 이상 사용되지 않습니다. 를 대신 사용 해야는 [getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int-sqlserverresultset.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.math.BigDecimal getBigDecimal(int columnIndex,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *소수 자릿수*  
  
 **int** 나타내는 소수점 오른쪽 자릿수입니다.  
  
## <a name="return-value"></a>반환 값  
 BigDecimal 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getBigDecimal 메서드는 java.sql.ResultSet 인터페이스의 getBigDecimal 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getBigDecimal 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
