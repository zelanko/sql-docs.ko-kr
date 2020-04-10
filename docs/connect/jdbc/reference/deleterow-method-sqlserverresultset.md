---
title: deleteRow 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c6f5cc2d3b58f553f74288c2c86e7b6d9d32d72
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922170"
---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow 메서드(SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체와 기본 데이터베이스에서 현재 행을 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
public void deleteRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 deleteRow 메서드는 java.sql.ResultSet 인터페이스의 deleteRow 메서드에 의해 지정됩니다.  
  
 커서가 삽입 행에 있는 경우에는 이 메서드를 호출할 수 없습니다.  
  
 키 집합 커서를 사용할 경우 이 메서드는 결과 세트에 간격을 남겨 둡니다. [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 메서드를 사용하여 이 간격을 테스트할 수 있습니다. 결과 집합에 포함된 행의 행 번호는 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
