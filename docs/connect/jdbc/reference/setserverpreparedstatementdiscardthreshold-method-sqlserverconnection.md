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
ms.openlocfilehash: 8f66746b15e96f49d96b428e8cf8844eeea12a12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972925"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>setServerPreparedStatementDiscardThreshold 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 특정 연결 인스턴스에 대 한 동작을 지정 합니다. 이 설정은 서버에서 처리 중인 핸들 정리에 대 한 호출이 실행 되기 전에 연결 당 처리 되지 않은 준비 된 문 삭제 작업 수 (sp_unprepare)를 제어 합니다. 설정이 < = 1 이면 준비 된 문 닫기에서 준비 취소 작업이 즉시 실행 됩니다. 값이 > 1로 설정 된 경우 이러한 호출은 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하기 위해 함께 일괄 처리 됩니다.


## <a name="syntax"></a>구문  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>매개 변수  
 *thresholdValue*  
 
 **ServerPreparedStatementDiscardThreshold** connection 속성의 새 값입니다.  
 
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4 및 이후 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
