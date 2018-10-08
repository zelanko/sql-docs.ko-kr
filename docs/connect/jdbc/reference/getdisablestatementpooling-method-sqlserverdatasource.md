---
title: getDisableStatementPooling 메서드 (SQLServerDataSource) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f7da0c0139af73e207a4aa28ae6e99fc291039da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634601"
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>getDisableStatementPooling 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  값을 반환 **disableStatementPooling** 연결 속성입니다. 이 설정은 문 풀링을 사용 하도록 설정할지 여부이 연결용 제어 합니다.

  
## <a name="syntax"></a>구문  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>반환 값  
 A **부울** 의 값이 포함 된 **disableStatementPooling** 연결 속성입니다.
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
