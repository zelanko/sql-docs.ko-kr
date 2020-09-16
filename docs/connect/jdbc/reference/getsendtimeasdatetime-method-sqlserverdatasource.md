---
description: getSendTimeAsDatetime 메서드(SQLServerDataSource)
title: getSendTimeAsDatetime 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8036454468143c5910d9b5d7ba8135cc1a0ec4a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434614"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 **sendTimeAsDatetime** 연결 속성의 설정을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>Return Value  
 java.sql.Time 값이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **날짜/시간** 형식으로 서버에 전송되는 경우 **true**입니다. java.sql.Time 값이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **시간** 형식으로 서버에 전송되는 경우 **false**입니다.  
  
## <a name="remarks"></a>설명  
 **sendTimeAsDatetime** 연결 속성에 대한 자세한 내용은 [연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)을 사용하면 **sendTimeAsDatetime** 연결 속성을 프로그래밍 방식으로 설정할 수 있습니다.  
  
 자세한 내용은 [java.sql.Time 값을 서버에 보내는 방식 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
