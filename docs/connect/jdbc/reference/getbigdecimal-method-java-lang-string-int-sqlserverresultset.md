---
title: getBigDecimal 메서드 (java.lang.String, int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBigDecimal (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 572a1799-c232-400f-b8d8-37a5719a8d5e
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e87292ffce36ccb9a4e1aa943938a328bde66f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getbigdecimal-method-javalangstring-int-sqlserverresultset"></a>getBigDecimal 메서드 (java.lang.String, int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 이름의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 지정 된 소수 자릿수를 사용 하 여 개체입니다.  
  
> [!NOTE]  
>  이 메서드는 JDBC 사양에서 더 이상 사용되지 않습니다. 를 대신 사용 해야는 [getBigDecimal (java.lang.String)](../../../connect/jdbc/reference/getbigdecimal-method-java-lang-string-sqlserverresultset.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String columnName,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
 *소수 자릿수*  
  
 **int** 나타내는 소수점 오른쪽 자릿수입니다.  
  
## <a name="return-value"></a>반환 값  
 BigDecimal 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getBigDecimal 메서드는 java.sql.ResultSet 인터페이스의 getBigDecimal 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getBigDecimal 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
