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
ms.openlocfilehash: c4774dcda174d5260289409053a892cc4039b4f0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980466"
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에 대한 참조를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>Return Value  
 참조 개체입니다.  
  
## <a name="remarks"></a>설명  
 이 getReference 메서드는 javax.naming.Referenceable 인터페이스의 getReference 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0 이전에는 SQLServerDataSource 개체에 대해 SQLServerDataSource.setTrustStorePassword가 호출된 경우 SQLServerDataSource.getReference에서 반환되는 개체에 암호가 제공되었으므로 이 개체를 사용하여 추가 연결을 만들 수 있었습니다. JDBC 드라이버 3.0에서는 SQLServerDataSource.getReference에서 반환되는 개체에 암호를 설정해야 이 개체를 사용하여 연결을 만들 수 있습니다.  
  
 또한 데이터 원본 속성을 바인딩하기 전에 SQLServerDataSource.setTrustStorePassword를 설정할 경우, 연결을 가져오기 전에 SQLServerDataSource.setTrustStorePassword를 호출해야 합니다. 예를 들면 다음과 같습니다.  
  
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
  
  
