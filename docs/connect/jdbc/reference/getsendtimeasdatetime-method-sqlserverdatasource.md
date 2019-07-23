---
title: getSendTimeAsDatetime 메서드 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1396ac28a7e41dbf530f7e4a251876f6c340871
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979938"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 **SendTimeAsDatetime** connection 속성의 설정을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>반환 값  
 java. 시간 값이 **날짜/** 시간 형식으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버에 전송 되는 경우 **true** 입니다. java. 시간 값이 **시간** 형식으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버에 전송 되는 경우 **false** 입니다.  
  
## <a name="remarks"></a>Remarks  
 **SendTimeAsDatetime** connection 속성에 대 한 자세한 내용은 [연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md) 을 참조 하세요.  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)을 사용하면 **sendTimeAsDatetime** 연결 속성을 프로그래밍 방식으로 설정할 수 있습니다.  
  
 자세한 내용은 [java. 시간 값을 서버로 보내는 방법 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
