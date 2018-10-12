---
title: finalize 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e1b8a5435d6923015c2d3c29eef5031f3d5b2f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622791"
---
# <a name="finalize-method-sqlserverresultset"></a>finalize 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 명시적으로 닫습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Remarks  
 응용 프로그램에서 결과 집합을 닫지 않는 경우 결과 집합을 닫습니다. 이 메서드는 단지 JDBC 사양을 따르기 위한 것입니다. JVM(Java Virtual Machine)에서는 언제 파이널라이저가 실행될 수 있는지를 보장하지 않으므로 결과 집합을 명시적으로 닫지 않은 응용 프로그램은 동일한 연결을 사용하며 행 잠금의 경우와 같이 공용 서버 리소스에서 차단된 다른 문에서 교착 상태가 될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
