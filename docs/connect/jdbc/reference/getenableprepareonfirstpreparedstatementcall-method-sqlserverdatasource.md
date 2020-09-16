---
description: getEnablePrepareOnFirstPreparedStatementCall 메서드(SQLServerDataSource)
title: getEnablePrepareOnFirstPreparedStatementCall 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 418e50a49972ba70a7e2ca85b57850c336935c78
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436075"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>getEnablePrepareOnFirstPreparedStatementCall 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **enablePrepareOnFirstPreparedStatementCall** 연결 속성의 값을 반환합니다. 이 구성이 false를 반환하는 경우, 준비된 문의 첫 번째 실행은 sp_executesql을 호출하고 문을 준비하지 않습니다. 두 번째 실행이 발생하면 sp_prepexec를 호출하고 실제로 준비된 문 핸들을 설정합니다. 다음 실행에서는 sp_execute를 호출합니다. 이렇게 하면 문이 한 번만 실행될 때 준비된 문 닫기에서 sp_unprepare를 사용할 필요가 없습니다. 
  
## <a name="syntax"></a>구문  
  
```
public boolean getEnablePrepareOnFirstPreparedStatementCall();  
```  
  
## <a name="return-value"></a>Return Value  
 **enablePrepareOnFirstPreparedStatementCall** 연결 속성의 **부울** 값을 반환합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>설명  
 이 메서드는 JDBC 드라이버 버전 6.4 이상 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
