---
title: isCaseSensitive 메서드 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isCaseSensitive
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4db67eb7-7ff2-4fb8-8052-39f699de53ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4fd8441858a186da9f5efa4b790d693ff4c78050
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834021"
---
# <a name="iscasesensitive-method-sqlserverresultsetmetadata"></a>isCaseSensitive 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열이 대/소문자를 구분하는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isCaseSensitive(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *column*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 열이 대/소문자를 구분하면 이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 isCaseSensitive 메서드는 java.sql.ResultSetMetaData 인터페이스의 isCaseSensitive 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
