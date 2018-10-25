---
title: isValid 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 855a2fc8c6ff5a1cb9cee1db7504e0dd309113b0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727451"
---
# <a name="isvalid-method-sqlserverconnection"></a>isValid 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 닫히지 않고 아직 유효한지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *timeout*  
  
 연결의 유효성을 검사하는 동안 대기하는 시간(초)을 지정하는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 연결이 유효하면 **true**이고, 연결이 유효하지 않거나 제한 시간이 만료되기 전에 연결의 유효성을 확인할 수 없으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 isValid 메서드는 java.sql.Connection 인터페이스의 isValid 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
