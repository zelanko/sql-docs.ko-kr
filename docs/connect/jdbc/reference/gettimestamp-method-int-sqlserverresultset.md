---
title: getTime 메서드(int)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTimestamp (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ad538a76-983f-4175-9481-9e7fa9480c71
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 286156070f62faa576eec11cb1f6d946420c7fb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823291"
---
# <a name="gettimestamp-method-int-sqlserverresultset"></a>getTimestamp 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 Java 프로그래밍 언어의 java.sql.Timestamp 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Timestamp getTimestamp(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 타임 스탬프 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getTime 메서드는 java.sql.ResultSet 인터페이스의 getTime 메서드에 의해 지정됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 및 smalldatetime 열에서만 값을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getTimestamp 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
