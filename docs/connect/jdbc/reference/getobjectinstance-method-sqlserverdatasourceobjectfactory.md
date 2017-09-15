---
title: "getObjectInstance 메서드 (SQLServerDataSourceObjectFactory) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d560f49aeb499c304028b3f2b317b2cb790faaa
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>getObjectInstance 메서드(SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 데이터 원본 개체의 인스턴스를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ref*  
  
 **개체** 값입니다.  
  
 *name*  
  
 개체 이름입니다.  
  
 *c*  
  
 지정된 이름에 상대적인 컨텍스트입니다.  
  
 *h*  
  
 개체를 만드는 데 사용되는 환경입니다.  
  
## <a name="return-value"></a>반환 값  
 **개체** 값입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>주의  
 이 getObjectInstance 메서드는 javax.naming.spi.ObjectFactory 인터페이스의 getObjectInstance 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSourceObjectFactory 메서드](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory 멤버](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory 클래스](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
