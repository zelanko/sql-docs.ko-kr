---
title: "unwrap 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c7fd1ebcd5f1a9a1d963298212b2423f90e194d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverdatasource"></a>unwrap 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  에 대 한 액세스를 허용 하도록 지정된 된 인터페이스를 구현 하는 개체를 반환 합니다.는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-특정 메서드.  
  
## <a name="syntax"></a>구문  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *iface*  
  
 인터페이스를 정의하는 T 형식의 클래스입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 인터페이스를 구현하는 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) 메서드는 JDBC 4.0 사양에서 도입 된 java.sql.Wrapper 인터페이스에 의해 정의 됩니다.  
  
 응용 프로그램에 관련 된 JDBC API에 대 한 확장에 액세스 해야 할 수는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다. Unwrap 메서드는이 개체가 확장 공급 업체 확장 노출 하는 경우 공용 클래스에 대 한 래핑 해제를 지원 합니다.  
  
 이 메서드가 호출 될 때 개체가 래핑 해제는 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스입니다.  
  
 자세한 내용은 참조 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [isWrapperFor 메서드 &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

