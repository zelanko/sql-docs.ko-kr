---
title: setServerPreparedStatementDiscardThreshold 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a2461ae9f0728971b54d033b2b215092becc0ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>setServerPreparedStatementDiscardThreshold 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 인스턴스를 특정 연결에 대 한 동작을 지정합니다. 이 설정은 개수 뛰어난 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출을 실행 하기 전에 작업 (sp_unprepare) 연결당 보류 될 수를 제어 합니다. 설정 < = 1 취소-준비 작업 준비 문에서 닫기 즉시 실행 됩니다. 값 1 >로 설정 된 경우 이러한 호출은 sp_unprepare를 너무 자주 호출의 오버 헤드를 방지 하기 위해 함께 일괄는 합니다.


## <a name="syntax"></a>구문  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>매개 변수  
 *thresholdValue*  
 
 새 값은 **serverPreparedStatementDiscardThreshold** 연결 속성입니다.  
 
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>주의  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
