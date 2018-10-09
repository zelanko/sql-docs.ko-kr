---
title: createSQLXML 메서드(SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.nativeSQL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2188a6e1-792f-47bd-b207-1d01741231b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 994a15cd8ac69c49306612582cb69413e035a1fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778491"
---
# <a name="nativesql-method-sqlserverconnection"></a>nativeSQL 메서드(SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 SQL 문을 데이터베이스 서버의 네이티브 SQL 문법으로 변환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 현재 이 메서드가 지원되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String nativeSQL(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 $**: SQL 문이 포함된 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 변환된 SQL 문이 들어 있는 입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 nativeSQL 메서드는 java.sql.Connection 인터페이스의 nativeSQL 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
