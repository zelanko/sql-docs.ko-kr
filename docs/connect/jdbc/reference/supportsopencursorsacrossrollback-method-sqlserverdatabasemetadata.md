---
title: supportsOpenCursorsAcrossRollback 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOpenCursorsAcrossRollback
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4bc3e82b-a7e7-43a5-8938-6f29c7570163
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a1dc525ba0d2be1a4bba4cdbee70365dfecc1bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840821"
---
# <a name="supportsopencursorsacrossrollback-method-sqlserverdatabasemetadata"></a>supportsOpenCursorsAcrossRollback 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 여러 번 롤백하는 동안 커서를 열어 둘 수 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsOpenCursorsAcrossRollback()  
```  
  
## <a name="return-value"></a>반환 값  
 **true** 지원 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 supportsOpenCursorsAcrossRollback 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsOpenCursorsAcrossRollback 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
