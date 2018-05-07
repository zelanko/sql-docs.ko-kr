---
title: updateBlob 메서드 (int, java.sql.Blob) | Microsoft Docs
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
- SQLServerResultSet.updateBlob (int, java.sql.Blob)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e86f588-1365-4011-9412-f0acf7009880
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0874832d98fef91d02e10000ea87a1f7110e5559
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="updateblob-method-int-javasqlblob"></a>updateBlob 메서드(int, java.sql.Blob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 java.sql.Blob 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBlob(int index,  
                       java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱스*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 Blob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateBlob 메서드는 java.sql.ResultSet 인터페이스의 updateBlob 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateBlob 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
