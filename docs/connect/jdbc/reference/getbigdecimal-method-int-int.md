---
title: Get이상 Decimal 메서드 (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d9351b35-7046-4852-a612-72d4c46b2bbb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77fa7092b7835e400b7ced8c7dbc0368188b0eb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954001"
---
# <a name="getbigdecimal-method-int-int"></a>getBigDecimal 메서드(int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스와 소수 자릿수가 지정된 경우 지정된 매개 변수의 값을 검색하여 java.math.BigDecimal로 반환합니다.  
  
> [!NOTE]  
>  이 메서드는 JDBC 사양에서 더 이상 사용되지 않습니다. 대신 [getBigDecimal(int)](../../../connect/jdbc/reference/getbigdecimal-method-int.md) 메서드를 사용해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
 *scale*  
  
 소수점 이하의 자릿수를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 가는 10 진수 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getBigDecimal 메서드는 java. CallableStatement 인터페이스의 Get이상 Decimal 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getBigDecimal 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
