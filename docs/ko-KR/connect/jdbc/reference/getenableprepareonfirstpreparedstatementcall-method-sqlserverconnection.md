---
title: getEnablePrepareOnFirstPreparedStatementCall 메서드 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b35678bdf98ee856bca40bfe1cb1b45ad680e2b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 메서드 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 값을 반환 **enablePrepareOnFirstPreparedStatementCall** 연결 속성입니다. 첫 번째 실행에서 sp_executesql을 호출 되며 준비 하지 false 인 경우 발생 하는 두 번째로 실행 되 면 한 문은 sp_prepexec 호출을 실제로 준비 된 문 핸들을 설정 합니다. 실행 될 때 다음 sp_execute를 호출 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되는 경우 됩니다. SetDefaultEnablePrepareOnFirstPreparedStatementCall() 호출 하 여이 옵션의 기본값을 변경할 수 있습니다.

## <a name="syntax"></a>구문  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>반환 값
 A **부울** 의 값이 포함 된 **enablePrepareOnFirstPreparedStatementCall** 연결 속성입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>주의  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
