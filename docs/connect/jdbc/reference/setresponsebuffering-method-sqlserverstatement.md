---
title: setResponseBuffering 메서드 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5b4490ac15558a0f6268a3d400d197367d028b9d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796751"
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>setResponseBuffering 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 응답 버퍼링 모드를 대/소문자를 구분하지 않는 **String full** 또는 **adaptive**로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *value*  
  
 응답 버퍼링 모드가 들어 있는 **String**입니다. 유효한 모드는 대/소문자를 구분하지 않는 문자열 **full** 또는 **adaptive**일 수 있습니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 **adaptive**는 필요할 때 가능한 최소한의 데이터를 버퍼링하도록 지정합니다.  
  
 **full**은 런타임에 서버의 전체 결과를 읽도록 지정합니다.  
  
 적응은 JDBC 드라이버 버전 2.0과 3.0의에서 기본값입니다. 전체 JDBC 드라이버 버전 2.0 이전는 기본값이 이었습니다.  
  
 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 사용하면 현재 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 **responseBuffering** 연결 **String** 속성을 재정의할 수 있습니다. 응답 버퍼링 모드를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [를 사용 하 여 선택 버퍼링](../../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
 애플리케이션에서 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드에 잘못된 매개 변수 값을 지정할 경우 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)이 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [적응 버퍼링 사용](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
