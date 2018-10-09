---
title: setString 메서드 (long, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a5fd1c9f0f876f024047fab5e28fb31ba29b687
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47839111"
---
# <a name="setstring-method-long-javalangstring"></a>setString 메서드(long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 String을 CLOB의 지정된 위치부터 씁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 CLOB에 쓰기 시작할 위치입니다.  
  
 *s*  
  
 CLOB에 쓸 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 쓴 문자 수입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 setString 메서드는 java.sql.Clob 인터페이스의 setString 메서드에 의해 지정 됩니다.  
  
 문자 데이터는 지정된 위치부터 덮어쓰여지며 CLOB의 초기 길이를 초과할 수 있습니다. 위치+1 값을 지정하면 문자열이 추가되고, 위치+2 이상(또는 0 이하)의 값을 지정하면 위치 오류가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [setString 메서드 &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
