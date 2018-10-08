---
title: setDisableStatementPooling 메서드 (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 4be547e1d5c37a00cd023bc542f3bb6e9f73e048
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611051"
---
# <a name="setdisablestatementpooling-method-sqlserverdatasource"></a>setDisableStatementPooling 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  값을 설정 합니다 **disableStatementPooling** 연결 속성입니다. False 이면 문을 풀링 statementPoolingCacheSize 값 > 0 인 결합에 사용할 수 있습니다.  

## <a name="syntax"></a>구문  
  
```
public void setDisableStatementPooling(boolean disableStatementPooling);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *disableStatementPooling*  
  
 새 값을 **disableStatementPooling** 연결 속성입니다.  

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 이 메서드는 JDBC 드라이버 버전 6.4에서에서 사용 가능 하 고 향후에.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
