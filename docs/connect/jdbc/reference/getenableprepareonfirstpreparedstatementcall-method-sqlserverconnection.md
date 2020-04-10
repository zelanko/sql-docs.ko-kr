---
title: getEnablePrepareOnFirstPreparedStatementCall 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 203ed2f6a68e11af8c63157a850a146ea8d81464
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909601"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 **enablePrepareOnFirstPreparedStatementCall** 연결 속성의 값을 반환합니다. false일 경우에는 첫 번째 실행에서 sp_executesql이 호출되고 문은 준비되지 않습니다. 두 번째 실행이 발생하면 sp_prepexec가 호출되고 준비된 문 핸들이 실제로 설정됩니다. 다음 실행에서는 sp_execute를 호출합니다. 이렇게 하면 문이 한 번만 실행될 때 준비된 문 닫기에서 sp_unprepare를 사용할 필요가 없습니다. 이 옵션의 기본값은 setDefaultEnablePrepareOnFirstPreparedStatementCall() 호출로 변경할 수 있습니다.

## <a name="syntax"></a>구문  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>Return Value
 **enablePrepareOnFirstPreparedStatementCall** 연결 속성 값이 포함된 **부울**입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>설명  
 이 메서드는 JDBC 드라이버 버전 6.4 이상 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
