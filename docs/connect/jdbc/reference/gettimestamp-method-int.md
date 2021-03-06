---
description: getTimestamp 메서드(int)
title: getTimestamp 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a9fd6496-c72e-4cc6-b46a-4aa9f13f90ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a8c8ffb622236d6bdff684686bef42ce6e3f02c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434075"
---
# <a name="gettimestamp-method-int"></a>getTimestamp 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 java.sql.Timestamp 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Timestamp getTimestamp(int index)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 Timestamp 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getTimestamp 메서드는 java.sql.CallableStatement 인터페이스의 getTimestamp 메서드에 의해 지정됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 및 **smalldatetime** 열에서만 값을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getTimestamp 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
