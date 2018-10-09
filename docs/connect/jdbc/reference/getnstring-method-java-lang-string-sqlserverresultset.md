---
title: getString 메서드(java.lang.String)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2fc3df07bcdb342b5796b6472d7e8b96ba1674b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826991"
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>getNString 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열의 값을 SQLXML 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블이 포함된 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 문자열 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 GetNString 메서드가 java.sql.SQLServerResultSet 인터페이스의 getNString 메서드에 의해 지정 됩니다.  
  
 값을 검색 하려면이 메서드를 사용할 수는 **nvarchar**를 **nchar**를 **nvarchar (max)** 를 **ntext**, 또는 **xml** 이 현재 행에서 열 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다. 이 메서드를 사용하여 다른 데이터 형식의 값을 검색하려고 하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getString 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
