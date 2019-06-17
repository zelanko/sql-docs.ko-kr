---
title: getColumnDisplaySize 메서드 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnDisplaySize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 21c25443-bd2b-4b60-9798-4efe2c158952
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: caf5b0a71fe179aa58da59a4434c485693939b9b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763585"
---
# <a name="getcolumndisplaysize-method-sqlserverresultsetmetadata"></a>getColumnDisplaySize 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열의 표준 최대 너비(문자 수)를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getColumnDisplaySize(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *column*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 최대 너비를 나타내는 **int**입니다. 너비를 알 수 없으면 0을 반환합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getColumnDisplaySize 메서드는 java.sql.ResultSetMetaData 인터페이스의 getColumnDisplaySize 메서드에 의해 지정 됩니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서는 COLUMN_SIZE 열의 동작이 변경되었습니다. 자세한 내용은 [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
