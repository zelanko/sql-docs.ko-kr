---
title: rowInserted 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowInserted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e7c10372-0be8-4baa-87f7-ed6b66003357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b52007528ee5c3d3caaabc83b158e50156b664e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67975689"
---
# <a name="rowinserted-method-sqlserverresultset"></a>rowInserted 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행에 삽입된 내용이 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean rowInserted()  
```  
  
## <a name="return-value"></a>Return Value  
 행에 삽입된 내용이 있고 삽입 내용이 검색되면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 rowUpdated 메서드는 java.sql.ResultSet 인터페이스의 rowUpdated 메서드에 의해 지정됩니다.  
  
 반환되는 값은 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체가 표시된 삽입 내용을 검색할 수 있는지 여부에 따라 달라집니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 모든 커서 유형에 대해 삽입된 행을 검색하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
