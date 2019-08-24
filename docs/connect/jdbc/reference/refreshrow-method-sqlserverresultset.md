---
title: refreshRow 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 570a9185a83ecf1af0e47ee25cce5445dca1b958
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975983"
---
# <a name="refreshrow-method-sqlserverresultset"></a>refreshRow 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스의 최신 값으로 현재 행을 새로 고칩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 refreshRow 메서드는 java. ResultSet 인터페이스의 refreshRow 메서드에 의해 지정 됩니다.  
  
 커서가 삽입 행에 있는 경우에는 이 메서드를 호출할 수 없습니다.  
  
 애플리케이션에서는 이 메서드를 통해 데이터베이스에서 행을 다시 인출하도록 JDBC 드라이버에 명시적으로 지정할 수 있습니다. [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]가 캐싱 또는 사전 인출 중일 때 애플리케이션에서 이 메서드를 호출하여 데이터베이스의 최신 행 값을 가져와야 할 수 있습니다. 인출 크기가 1보다 크면 JDBC 드라이버에서는 실제로 여러 개의 행을 동시에 새로 고칠 수 있습니다.  
  
 모든 값은 트랜잭션 격리 수준과 커서 민감도에 따라 다시 인출됩니다. updater 메서드를 호출한 후 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 메서드를 호출하기 전에 이 메서드를 호출하면 행에 대한 업데이트 내용을 잃게 됩니다. 이 메서드를 자주 호출하면 성능이 저하될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
