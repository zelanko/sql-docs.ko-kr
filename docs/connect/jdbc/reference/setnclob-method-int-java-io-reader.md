---
title: setNClob 메서드(int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9fc9938c-b821-41c7-8df7-e21cb83a46d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4abac6b892ae5960e8cafc5f265d6a81081e878b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67973777"
---
# <a name="setnclob-method-int-javaioreader"></a>setNClob 메서드(int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 Reader 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNClob(int parameterIndex,  
                    java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
 *reader*  
  
 매개 변수 값을 나타내는 Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setNClob 메서드는 java.sql.PreparedStatement 인터페이스의 setNClob 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNClob 메서드(SQLServerPreparedStatement)](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
