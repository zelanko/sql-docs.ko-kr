---
title: setAsciiStream 메서드(int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02c2443d-44e1-4f16-a0d5-08d197838214
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5520e84dc049a3aa395e62b4df94331d50fd8d63
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711361"
---
# <a name="setasciistream-method-int-javaioinputstream"></a>setAsciiStream 메서드(int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 java.io.InputStream 개체에 지정 된 매개 변수 번호를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *된*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *x*  
  
 Java.io.InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setAsciiStream 메서드는 java.sql.PreparedStatement 인터페이스의 setAsciiStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setAsciiStream 메서드(SQLServerPreparedStatement)](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
