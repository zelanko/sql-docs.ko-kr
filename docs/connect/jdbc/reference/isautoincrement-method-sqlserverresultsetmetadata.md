---
title: isAutoIncrement 메서드 (SQLServerResultSetMetaData) | Microsoft Docs
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
- SQLServerResultSetMetaData.isAutoIncrement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 028b8d61-9557-4c9f-b732-29e87a962de8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a81d4b4e2b12fb25888c76cfc6dc7c2010f56ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32840288"
---
# <a name="isautoincrement-method-sqlserverresultsetmetadata"></a>isAutoIncrement 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열이 자동으로 번호가 매겨지고 이로 인해 읽기 전용이 되는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isAutoIncrement(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *column*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 열 번호가 자동으로 매겨 지 면 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 isAutoIncrement 메서드는 java.sql.ResultSetMetaData 인터페이스의 isAutoIncrement 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
