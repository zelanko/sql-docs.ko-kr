---
title: updateBlob 메서드(java.lang.String, java.sql.Blob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBlob (java.lang.String, java.sql.Blob)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fdd47885-c7ec-4599-a645-ad0e082586f4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81d089b7a0cd2d052be6df55791559f4a45aa1b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674092"
---
# <a name="updateblob-method-javalangstring-javasqlblob"></a>updateBlob 메서드(java.lang.String, java.sql.Blob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 java.sql.Blob 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateBlob(java.lang.String columnName,  
                       java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
 *x*  
  
 Blob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateBlob 메서드는 java.sql.ResultSet 인터페이스의 updateBlob 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateBlob 메서드(SQLServerResultSet)](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
