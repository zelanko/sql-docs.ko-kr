---
title: getObject 메서드(int)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getObject (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 94e59366-ca34-4cd5-a6ec-ae32d475ef36
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 69ea6db0c79840f1bcdea0605611cdfa853055a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787680"
---
# <a name="getobject-method-int-sqlserverresultset"></a>getObject 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 Java 프로그래밍 언어의 개체로 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.Object getObject(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 **Object** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getObject 메서드는 java.sql.ResultSet 인터페이스의 getObject 메서드에 의해 지정됩니다.  
  
 이 메서드는 지정된 열의 값을 Java 개체로 반환합니다. Java 개체의 형식은 열의 SQL 형식에 해당하는 기본 Java 개체 형식으로서, JDBC 사양에 지정된 기본 제공 형식에 대한 매핑을 따릅니다. 값이 SQL NULL이면 드라이버에서는 Java null을 반환합니다.  
  
 이 메서드는 데이터베이스 관련 추상 데이터 형식을 읽는 데에도 사용할 수 있습니다. JDBC 2.0 API에서는 getObject 메서드의 동작이 확장되어 SQL 사용자 정의 형식의 데이터를 구체화합니다. 열에 구조화되었거나 고유한 값이 들어 있는 경우 이 메서드는 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`를 호출할 때와 동일하게 동작합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터는 다음과 같은 결과가 나타납니다.  
  
-   date 형식의 값은 java.sql.Date 개체로 반환됩니다.  
  
-   time 형식의 값은 java.sql.Time 개체로 반환됩니다.  
  
-   datetime2 형식의 값은 java.sql.Timestamp 개체로 반환됩니다.  
  
-   datetimeoffset 형식의 값은 microsoft.sql.DateTimeOffset 개체로 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getObject 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
