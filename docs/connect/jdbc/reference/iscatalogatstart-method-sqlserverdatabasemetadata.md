---
title: isCatalogAtStart 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.isCatalogAtStart
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 665173d2-14c7-4ce1-954e-4adb53fb9b39
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d81803b9e10a635b168fd1aed20a242fdf2dd80e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32839938"
---
# <a name="iscatalogatstart-method-sqlserverdatabasemetadata"></a>isCatalogAtStart 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  카탈로그가 정규화된 테이블 이름의 처음에 나타나는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isCatalogAtStart()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 카탈로그 이름이 처음에 나타나면 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 isCatalogAtStart 메서드는 java.sql.DatabaseMetaData 인터페이스의 isCatalogAtStart 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
