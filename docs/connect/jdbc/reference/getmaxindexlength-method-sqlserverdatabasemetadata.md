---
title: getMaxIndexLength 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxIndexLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c85d021-d466-4732-85f9-53903d297041
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5f2528fc47c2196cd542f51abbe86f673d14f6e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827781"
---
# <a name="getmaxindexlength-method-sqlserverdatabasemetadata"></a>getMaxIndexLength 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스가 인덱스(인덱스의 모든 부분 포함)에 허용하는 최대 바이트 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getMaxIndexLength()  
```  
  
## <a name="return-value"></a>반환 값  
 허용되는 최대 바이트 수를 나타내는 int입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getMaxIndexLength 메서드는 java.sql.DatabaseMetaData 인터페이스의 getMaxIndexLength 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
