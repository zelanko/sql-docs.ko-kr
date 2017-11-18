---
title: "없으면에서 개체 닫기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ce8f9b35-c761-4b0c-9a46-985eef2c2e0b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e742eeca533633d1055315a14b1c4f76c061be81
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="closing-objects-when-not-in-use"></a>개체가 사용되고 있지 않을 때 닫기
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  개체를 사용 하 여 작업할 때 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 특히 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 와 같은 개체는 문 중 하나 또는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement ](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), 더 이상 필요 없는 경우에 닫기 메서드를 사용 하 여 명시적으로 닫을 해야 합니다. 이를 통해 Java Virtual Machine 가비지 수집기가 비울 때까지 기다리는 대신 가능한 빨리 드라이버 및 서버 리소스를 비워 성능이 향상됩니다.  
  
 개체 닫기는 스크롤 잠금을 사용할 때 서버에서 훌륭한 동시성을 유지 관리하는 데 특히 중요합니다. 마지막을 액세스한 인출 버퍼의 스크롤 잠금은 결과 집합이 닫힐 때까지 보존됩니다. 이와 유사하게 명령문 준비 핸들은 문이 닫힐 때까지 보존됩니다. 여러 명령문에 대한 연결을 다시 사용할 경우 범위 밖으로 벗어나게 하기 전에 명령문을 닫으면 서버가 준비 핸들을 이전에 정리할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

