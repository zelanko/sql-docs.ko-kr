---
title: "getServerPreparedStatementDiscardThreshold 메서드 (SQLServerConnection) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 680c7fe2fe0802054f56008701af48baea4ac98b
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 값을 반환 **serverPreparedStatementDiscardThreshold** 연결 속성입니다. 이 설정은 개수 뛰어난 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출을 실행 하기 전에 작업 (sp_unprepare) 연결당 보류 될 수를 제어 합니다. 설정 되어 있으면 < = 1, unprepare 준비 문에서 닫기 작업이 즉시 실행 됩니다. > 1로 설정 하면 이러한 호출이 sp_unprepare를 너무 자주 호출의 오버 헤드를 방지 하기 위해 일괄 됩니다. GetDefaultServerPreparedStatementDiscardThreshold() 호출 하 여이 옵션의 기본값을 변경할 수 있습니다.

## <a name="syntax"></a>구문  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>반환 값
 **int** 의 값이 포함 된 **serverPreparedStatementDiscardThreshold** 연결 속성입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>주의  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
