---
title: setServerPreparedStatementDiscardThreshold 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a0105f615a123aa9ec4a4d329601c7992f76469
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845238"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>setServerPreparedStatementDiscardThreshold 메서드 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ServerPreparedStatementDiscardThreshold 연결 속성의 값을 설정 합니다. 이 설정은 개수 뛰어난 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출을 실행 하기 전에 작업 (sp_unprepare) 연결당 보류 될 수를 제어 합니다. 설정 < = 1 준비 작업 준비 문에서 닫기 즉시 실행 됩니다. 이러한 호출은 내용이 sp_unprepare를 너무 자주 호출의 오버 헤드를 방지 하기 위해 함께 일괄 처리 값 > 1로 설정 된 경우
 
## <a name="syntax"></a>구문  
  
```
public void setServerPreparedStatementDiscardThreshold(int enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *serverPreparedStatementDiscardThreshold*  
  
 새 값은 **serverPreparedStatementDiscardThreshold** 연결 속성입니다.  

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>주의  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
