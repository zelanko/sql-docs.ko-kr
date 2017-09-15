---
title: "isCurrency 메서드 (SQLServerResultSetMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSetMetaData.isCurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7fe25d90-693c-4d3b-9dd2-0f8351c5a9ed
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d174c5a63cf47ef53eb05634a94ea5506001db4e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="iscurrency-method-sqlserverresultsetmetadata"></a>isCurrency 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열이 현금 값인지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isCurrency(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *열*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 열이 현금 값입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 isCurrency 메서드는 java.sql.ResultSetMetaData 인터페이스의 isCurrency 메서드에 의해 지정 됩니다.  
  
 이 메서드는 반환 **true** 에서만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] money 및 smallmoney 데이터 형식입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
