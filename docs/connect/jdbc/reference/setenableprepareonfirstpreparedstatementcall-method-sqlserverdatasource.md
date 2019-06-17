---
title: setEnablePrepareOnFirstPreparedStatementCall 메서드 (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 18cd626fb3eee4690d87dd40edd50e64a4dcd98e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779140"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>setEnablePrepareOnFirstPreparedStatementCall 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  특정 연결 인스턴스에 대 한 동작을 지정 합니다. 이 구성을 준비 된 문을 첫 번째 실행 되며 sp_executesql을 호출 하지는 문 준비를 두 번째 실행 sp_prepexec를 호출 하 고 준비 된 문 핸들을 실제로 설치 되 면 false 인 경우 다음 실행 sp_execute를 호출 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되 면 됩니다.  
## <a name="syntax"></a>구문  
  
```
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 새 값을 **enablePrepareOnFirstPreparedStatementCall** 연결 속성입니다.  

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
