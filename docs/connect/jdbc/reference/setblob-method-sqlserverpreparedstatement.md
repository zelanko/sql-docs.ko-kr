---
title: setBlob 메서드(SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 218ff486-3f31-49e4-ad81-a423246a8307
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 971bfea1d1b2d0d113bd4b49215a37be1320fdc5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643531"
---
# <a name="setblob-method-sqlserverpreparedstatement"></a>setBlob 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 Blob 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setBlob(int i,  
                          java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *i*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *x*  
  
 Blob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setBlob 메서드는 java.sql.PreparedStatement 인터페이스의 setBlob 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
