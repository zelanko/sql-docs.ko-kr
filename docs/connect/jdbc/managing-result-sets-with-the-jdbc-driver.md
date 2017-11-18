---
title: "JDBC 드라이버 집합 결과 관리 | Microsoft Docs"
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
ms.assetid: 9ed5ad41-22e0-4e4a-8a79-10512db60d50
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e17e39f8a83313a60b269fed82631b80f07ffed5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="managing-result-sets-with-the-jdbc-driver"></a>JDBC 드라이버로 결과 집합 관리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  결과 집합은 대개 쿼리의 결과로 데이터 원본에서 반환되는 데이터의 집합을 나타내는 개체입니다. 결과 집합은 요청한 데이터 요소를 보유하는 행과 열을 포함하며 커서를 사용하여 탐색합니다. 결과 집합은 업데이트할 수 있으므로 수정할 수 있을 뿐 아니라 이러한 수정 내용을 원래의 데이터 원본에 적용할 수도 있습니다. 또한 결과 집합에는 기본 데이터 원본의 변경 내용에 따른 중요도 수준이 다양하게 있습니다.  
  
 문을 만들 때 호출 되는 경우 결과 집합의 유형을 결정 됩니다는 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스 이루어집니다. 결과 집합의 기본 역할은 Java 응용 프로그램에 사용 가능한 데이터베이스 데이터의 표현을 제공하는 것입니다. 이는 대개 결과 집합 데이터 요소에 대해 형식화된 getter 및 setter 메서드를 사용하여 수행합니다.  
  
 다음 예제를 기반으로 하는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 결과 집합을 호출 하 여 만듭니다는 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다. 결과 집합에서 데이터를 사용 하 여 표시 됩니다는 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
 [!code[JDBC#ManagingResultSets1](../../connect/jdbc/codesnippet/Java/managing-result-sets-with-t_1.java)]  
  
 이 섹션의 항목에서는 커서 유형, 동시성 및 행 잠금을 비롯하여 결과 집합 사용의 다양한 측면에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[커서 유형 이해](../../connect/jdbc/understanding-cursor-types.md)|여러 가지에 대해 설명 하는 커서 유형에 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 지원 합니다.|  
|[동시성 제어 이해](../../connect/jdbc/understanding-concurrency-control.md)|JDBC 드라이버에서 동시성 제어를 지원하는 방법을 설명합니다.|  
|[행 잠금 이해](../../connect/jdbc/understanding-row-locking.md)|JDBC 드라이버에서 행 잠금을 지원하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

