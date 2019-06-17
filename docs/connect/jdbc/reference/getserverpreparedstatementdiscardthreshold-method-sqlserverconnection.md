---
title: getServerPreparedStatementDiscardThreshold 메서드 (SQLServerConnection) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 22f7bf637d20b42a7dadd3397e84c826fa277a22
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66791921"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 값을 반환 **serverPreparedStatementDiscardThreshold** 연결 속성입니다. 이 설정은 얼마나 많은 처리 중인 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출 실행 되기 전에 작업 (sp_unprepare) 연결 별로 처리 하지 않을 수를 제어 합니다. 설정 되어 있으면 < = 1, unprepare 준비 된 문에서 닫기 작업이 즉시 실행 됩니다. > 1로 설정 된 경우 이러한 호출은 함께 일괄 처리 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하려면. 호출 getDefaultServerPreparedStatementDiscardThreshold() 하 여이 옵션의 기본값을 변경할 수 있습니다.

## <a name="syntax"></a>구문  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>반환 값
 **int** 의 값이 포함 된 **serverPreparedStatementDiscardThreshold** 연결 속성입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
