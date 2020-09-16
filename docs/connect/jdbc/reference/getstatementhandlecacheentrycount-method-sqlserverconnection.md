---
description: getStatementHandleCacheEntryCount 메서드(SQLServerConnection)
title: getStatementHandleCacheEntryCount 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getStatementHandleCacheEntryCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c722c6454be649372ba6bb97eaf5f477965a885e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434385"
---
# <a name="getstatementhandlecacheentrycount-method-sqlserverconnection"></a>getStatementHandleCacheEntryCount 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 현재 풀링된 준비 문 핸들의 수를 반환합니다.

## <a name="syntax"></a>구문  
  
```  
  
public int getStatementHandleCacheEntryCount()  
```  

## <a name="return-value"></a>Return Value
 풀링된 준비된 문 핸들의 현재 수를 포함하는 **int**입니다.

## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>설명  
 이 메서드는 JDBC 드라이버 버전 6.4 이상 버전에서 사용할 수 있습니다.
 
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
