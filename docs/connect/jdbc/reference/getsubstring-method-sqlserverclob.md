---
title: getSubString 메서드(SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getSubString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf915590-a883-4403-befa-5b5bb42f34d8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3404d7e31cdc5ed82a4a2c57af1a05354104d4bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66787451"
---
# <a name="getsubstring-method-sqlserverclob"></a>getSubString 메서드(SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 시작 위치 및 복사할 문자 수에 따라 CLOB에서 지정된 부분 문자열의 복사본을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *pos*  
  
 추출할 부분 문자열의 첫 번째 문자입니다. 첫 번째 문자는 위치 1에 있습니다.  
  
 *length*  
  
 복사할 연속된 문자의 수입니다.  
  
## <a name="return-value"></a>반환 값  
 CLOB에서 지정된 부분 문자열인 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getSubString 메서드 java.sql.Clob 인터페이스의 getSubString 메서드에 의해 지정됩니다.  
  
 null 또는 길이가 0인 CLOB에서 0개의 문자를 가져오려고 하면 빈 문자열이 반환됩니다. 길이가 0인 CLOB에서 위치 1이 아닌 다른 위치에 있는 임의 길이의 문자를 가져오려고 하면 위치 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
