---
title: getReference 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33a1b82b5855447df7e9b55c7506e87f6ffb8f2a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825999"
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에 대한 참조를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>반환 값  
 참조 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 이 getReference 메서드는 javax.naming.Referenceable 인터페이스의 getReference 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0 이전에는 SQLServerDataSource 개체에 대해 SQLServerDataSource.setTrustStorePassword가 호출된 경우 SQLServerDataSource.getReference에서 반환되는 개체에 암호가 제공되었으므로 이 개체를 사용하여 추가 연결을 만들 수 있었습니다. JDBC 드라이버 3.0에서는 SQLServerDataSource.getReference에서 반환되는 개체에 암호를 설정해야 이 개체를 사용하여 연결을 만들 수 있습니다.  
  
 또한 데이터 원본 속성을 바인딩하기 전에 SQLServerDataSource.setTrustStorePassword를 설정할 경우, 연결을 가져오기 전에 SQLServerDataSource.setTrustStorePassword를 호출해야 합니다. 예:  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
