---
title: getEnablePrepareOnFirstPreparedStatementCall 메서드 (SQLServerConnection) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ac1cf4dbd8c8c14b5c97dbfecbe81d397c1598ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983447"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 **EnablePrepareOnFirstPreparedStatementCall** connection 속성의 값을 반환 합니다. False 이면 첫 번째 실행에서 sp_executesql을 호출 하 고 문을 준비 하지 않습니다. 두 번째 실행이 발생 하면 sp_prepexec를 호출 하 고 실제로 준비 된 문 핸들을 설정 합니다. 다음 실행은 sp_execute를 호출 합니다. 이렇게 하면 문이 한 번만 실행 되는 경우 준비 된 문에 대 한 sp_unprepare 필요 하지 않습니다. 이 옵션의 기본값은 setDefaultEnablePrepareOnFirstPreparedStatementCall ()를 호출 하 여 변경할 수 있습니다.

## <a name="syntax"></a>구문  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>반환 값
 **EnablePrepareOnFirstPreparedStatementCall** connection 속성의 값을 포함 하는 **부울** 입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4 및 이후 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
