---
title: setServerPreparedStatementDiscardThreshold 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fb2962f6514fec7211b6d3a5ccd5f3af09a1f066
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782922"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>setServerPreparedStatementDiscardThreshold 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ServerPreparedStatementDiscardThreshold 연결 속성의 값을 설정 합니다. 이 설정은 얼마나 많은 처리 중인 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출 실행 되기 전에 작업 (sp_unprepare) 연결 별로 처리 하지 않을 수를 제어 합니다. 설정의 경우 < = 1 unprepare 작업 준비 된 문에서 닫기 즉시 실행 됩니다. Sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하려면 이러한 호출은 함께 일괄 처리 값 > 1로 설정 된 경우
 
## <a name="syntax"></a>구문  
  
```
public void setServerPreparedStatementDiscardThreshold(int enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *serverPreparedStatementDiscardThreshold*  
  
 새 값을 **serverPreparedStatementDiscardThreshold** 연결 속성입니다.  

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
