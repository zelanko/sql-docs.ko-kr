---
title: supportsMultipleTransactions 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMultipleTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 34ff8dcb-5487-46d1-a4c1-25e33eb3eee4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d984d5cf52ad0bc5b5b58df6914d00ef7722b8a4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764125"
---
# <a name="supportsmultipletransactions-method-sqlserverdatabasemetadata"></a>supportsMultipleTransactions 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 여러 개의 트랜잭션이 서로 다른 연결에서 동시에 열려 있을 수 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsMultipleTransactions()  
```  
  
## <a name="return-value"></a>반환 값  
 **true** 지원 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 supportsMultipleTransactions 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsMultipleTransactions 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
