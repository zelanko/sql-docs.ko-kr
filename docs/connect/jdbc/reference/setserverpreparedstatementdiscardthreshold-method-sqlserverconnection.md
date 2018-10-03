---
title: setServerPreparedStatementDiscardThreshold 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d008e26d4eb7e6c2ac4b362f03ce3b2716a4cc46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655031"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>setServerPreparedStatementDiscardThreshold 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 특정 연결 인스턴스에 대 한 동작을 지정 합니다. 이 설정은 얼마나 많은 처리 중인 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출 실행 되기 전에 작업 (sp_unprepare) 연결 별로 처리 하지 않을 수를 제어 합니다. 설정의 경우 < = 1 취소-준비 작업 준비 된 문에서 닫기 즉시 실행 됩니다. 값 > 1로 설정 된 경우 이러한 호출은 함께 일괄 처리 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하려면.


## <a name="syntax"></a>구문  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>매개 변수  
 *thresholdValue*  
 
 새 값을 **serverPreparedStatementDiscardThreshold** 연결 속성입니다.  
 
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
