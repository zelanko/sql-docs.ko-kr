---
title: "ISQLServerPreparedStatement 인터페이스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf87892e-5c34-4ac6-8258-c2a81e117b26
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56f10262ce0f55434419600299fb12961d9be15b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="isqlserverpreparedstatement-interface"></a>ISQLServerPreparedStatement 인터페이스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC의 준비된 문 기능에 대한 기본 구현을 나타냅니다. 이 인터페이스에 추가 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 **패키지에 대 한** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.sql.PreparedStatement, [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
public interface ISQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>주의  
 이 인터페이스는 구현 하 여 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)합니다.  
  
 이 인터페이스를 노출 다음 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-특정 메서드:  
  
|메서드|자세한 내용은 다음을 참조하세요.|  
|------------|-------------------------------|  
|public void setDateTimeOffset(int, microsoft.sql.DateTimeOffset)|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
