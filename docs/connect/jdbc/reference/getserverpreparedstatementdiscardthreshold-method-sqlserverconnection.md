---
title: getServerPreparedStatementDiscardThreshold 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 844f4574fa7a0a45c772a3ac3eff57bb91f23c3b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925353"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 **serverPreparedStatementDiscardThreshold** 연결 속성의 값을 반환합니다. 이 설정은 서버의 미처리 핸들을 정리하기 위한 호출 실행 전에 연결별로 처리되지 않을 수 있는 미처리 준비 문 삭제 작업(sp_unprepare)의 수를 제어합니다. 설정이 <= 1로 되어 있다면 준비된 문이 종료되자마자 준비 취소 작업이 곧바로 실행됩니다. 설정이 > 1로 되어 있다면 이러한 호출은 sp_unprepare 호출이 너무 잦아지는 오버헤드를 방지하기 위해 모두 함께 일괄 처리됩니다. 이 옵션의 기본값은 getDefaultServerPreparedStatementDiscardThreshold() 호출로 변경할 수 있습니다.

## <a name="syntax"></a>구문  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>Return Value
 **serverPreparedStatementDiscardThreshold** 연결 속성의 값을 포함하는 **int**입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>설명  
 이 메서드는 JDBC 드라이버 버전 6.4 이상 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
