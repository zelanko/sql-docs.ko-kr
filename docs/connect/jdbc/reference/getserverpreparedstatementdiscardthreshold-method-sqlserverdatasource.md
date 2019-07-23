---
title: getServerPreparedStatementDiscardThreshold 메서드 (SQLServerDataSource) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979900"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **ServerPreparedStatementDiscardThreshold** connection 속성의 값을 반환 합니다. 이 설정은 서버에서 처리 중인 핸들 정리에 대 한 호출이 실행 되기 전에 연결 당 처리 되지 않은 준비 된 문 삭제 작업 수 (sp_unprepare)를 제어 합니다. 설정이 < = 1 이면 준비 된 문 종료 시 작업이 즉시 실행 됩니다. 이 값을 > 1로 설정 하면 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하기 위해 이러한 호출을 함께 일괄 처리 합니다.

  
## <a name="syntax"></a>구문  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>반환 값  
 **ServerPreparedStatementDiscardThreshold** connection 속성의 **int** 값을 반환 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4 및 이후 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
