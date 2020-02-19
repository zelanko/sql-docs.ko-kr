---
title: getServerPreparedStatementDiscardThreshold 메서드(SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 3f91b75b5c70029d53582b8b6ed4655485fd3fcf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979900"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **serverPreparedStatementDiscardThreshold** 연결 속성의 값을 반환합니다. 이 설정은 서버의 미처리 핸들을 정리하기 위한 호출 실행 전에 연결별로 처리되지 않을 수 있는 미처리 준비 문 삭제 작업(sp_unprepare)의 수를 제어합니다. 설정이 <= 1로 되어 있을 때에는 준비된 문이 종료되자마자 준비 취소 작업이 곧바로 실행됩니다. 값이 > 1로 설정되어 있다면 이러한 호출은 sp_unprepare 호출이 너무 잦아지는 오버헤드를 방지하기 위해 모두 함께 일괄 처리됩니다.

  
## <a name="syntax"></a>구문  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Return Value  
 **serverPreparedStatementDiscardThreshold** 연결 속성의 **int** 값이 반환됩니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>설명  
 이 메서드는 JDBC 드라이버 버전 6.4 및 이후 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
