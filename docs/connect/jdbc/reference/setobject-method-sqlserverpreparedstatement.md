---
title: setObject 메서드(SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93a2b22c-82b4-48c7-a428-369ebe98a372
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27993632c5aa6f1ab334c02c123a1984d3408b6e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67973288"
---
# <a name="setobject-method-sqlserverpreparedstatement"></a>setObject 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 개체를 사용하여 지정된 매개 변수의 값을 설정합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터 이 메서드의 동작은 **sendTimeAsDatetime** 연결 속성([연결 속성 설정](../../../connect/jdbc/setting-the-connection-properties.md)) 및 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)에 의해 수정됩니다.  
  
 자세한 내용은 [java.sql.Time 값을 서버에 보내는 방식 구성](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)을 참조하세요.  
  
## <a name="overload-list"></a>오버로드 목록  
  
|속성|Description|  
|----------|-----------------|  
|[setObject(int, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object.md)|지정된 개체를 사용하여 지정된 매개 변수의 값을 설정합니다.|  
|[setObject(int, java.lang.Object, int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int.md)|지정된 개체와 대상 형식을 사용하여 지정된 매개 변수의 값을 설정합니다.|  
|[setObject(int, java.lang.Object, int, int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int-int.md)|지정된 개체, 대상 형식 및 소수 자릿수를 사용하여 지정된 매개 변수의 값을 설정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
