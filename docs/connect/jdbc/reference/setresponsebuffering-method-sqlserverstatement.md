---
title: "setResponseBuffering 메서드 (SQLServerStatement) | Microsoft Docs"
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
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c5af0e179ea15fc4d5a30604b606f5ff45c79a1b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>setResponseBuffering 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  응답 버퍼링 모드를이 대 한 설정 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 대/소문자 구분 **문자열 전체** 또는 **적응**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *value*  
  
 A **문자열** 응답 버퍼링 모드를 포함 하 합니다. 유효한 모드는 다음과 같은 대/소문자 구분 문자열 중 하나일 수 있습니다: **전체** 또는 **적응**합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 **적응** 필요할 때 최소 가능한 데이터를 버퍼링 하도록 지정 합니다.  
  
 **전체** 런타임 시 서버에서 전체 결과 읽도록 지정 합니다.  
  
 적응은 JDBC 드라이버 버전 2.0과 3.0의 기본 값입니다. JDBC 드라이버 버전 2.0 이전 기본 전체 했습니다.  
  
 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 사용 하면 재정의 하는 **responseBuffering** 연결 **문자열** 속성에 대 한 현재 [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체입니다. 응답 버퍼링 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
 응용 프로그램에 잘못 된 매개 변수 값을 지정 하는 경우는 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 한 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) throw 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [적응 버퍼링 사용](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  

