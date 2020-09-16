---
description: isStatementPoolingEnabled 메서드(SQLServerConnection)
title: isStatementPoolingEnabled 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.isStatementPoolingEnabled
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 76c6afdec909de1edce177e05599b37b4fa8c746
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433365"
---
# <a name="isstatementpoolingenabled-method-sqlserverconnection"></a>isStatementPoolingEnabled 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 이 연결에 대한 문 풀링의 사용 설정 여부를 반환합니다.

## <a name="syntax"></a>구문  
  
```  
  
public boolean isStatementPoolingEnabled()  
```  

## <a name="return-value"></a>Return Value
 문 풀링의 사용 설정 여부를 나타내는 플래그를 포함하는 **boolean**입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>설명  
 이 메서드는 JDBC 드라이버 버전 6.4 이상 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
