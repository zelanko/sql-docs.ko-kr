---
title: getColumnClassName 메서드(SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2c118790-5dd2-4b10-93b6-7f065ee324ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79421c39ba134a801d9c0de3bba3c7a7ec00b718
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924493"
---
# <a name="getcolumnclassname-method-sqlserverresultsetmetadata"></a>getColumnClassName 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md) 클래스의 [getObject](../../../connect/jdbc/reference/sqlserverresultset-class.md) 메서드를 호출하여 열에서 값을 검색할 경우 인스턴스가 생성되는 Java 클래스의 정규화된 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getColumnClassName(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *column*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 클래스의 정규화된 이름이 들어 있는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getColumnClassName 메서드는 java.sql.ResultSetMetaData 인터페이스의 getColumnClassName 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
