---
title: setSendTimeAsDatetime 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a5e9d17255ac790fbf2d1466555a2e2e877e13d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>setSendTimeAsDatetime 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는에서 추가 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 설정을 수정 된 **sendTimeAsDatetime** 연결 속성입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sendTimeAsDateTime*  
  
 부울 값입니다. True 이면 java.sql.Time 값이 서버에 보낼 수로 인해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** 형식입니다. False 인 경우 java.sql.Time 값이 서버에 보낼 수로 인해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **시간** 형식입니다.  
  
## <a name="remarks"></a>주의  
 [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) 의 설정을 반환 하는 **sendTimeAsDatetime** 연결 속성입니다.  
  
 대 한 자세한 내용은 **sendTimeAsDatetime** 연결 속성 참조 [연결 속성을 설정할](../../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 자세한 내용은 참조 [구성 방법을 java.sql.Time 값에는 서버에 보내집니다](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
