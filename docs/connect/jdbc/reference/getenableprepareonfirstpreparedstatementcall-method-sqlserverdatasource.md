---
title: "getEnablePrepareOnFirstPreparedStatementCall 메서드 (SQLServerDataSource) | Microsoft Docs"
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
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 766a00c0a92c3df65e39bbfcd7ad87c5529a5b98
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>getEnablePrepareOnFirstPreparedStatementCall 메서드 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  값을 반환 **enablePrepareOnFirstPreparedStatementCall** 연결 속성입니다. 이 구성은 false를 반환 합니다. 준비 된 문을 첫 번째 실행에서 sp_executesql을 호출 되며 sp_prepexec를 호출 하 고 준비 된 문 핸들을 실제로 설치 발생 하는 두 번째로 실행 되 면 문을 준비 하지 됩니다. 실행 될 때 다음 sp_execute를 호출 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되는 경우 됩니다. 
  
## <a name="syntax"></a>구문  
  
```
public boolean getEnablePrepareOnFirstPreparedStatementCall();  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **부울** 값은 **enablePrepareOnFirstPreparedStatementCall** 연결 속성입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>주의  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
