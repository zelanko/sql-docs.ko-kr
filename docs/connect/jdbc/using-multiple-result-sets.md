---
title: "여러 결과 집합을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e76f30f5c6b7eb16351749086173bdceaa49f938
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="using-multiple-result-sets"></a>다중 결과 집합 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  SQL 인라인 작업할 때 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 둘 이상의 결과 집합을 반환 하는 저장 프로시저는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 제공는 [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 에서 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스 반환 된 데이터의 각 집합을 검색 합니다. 또한 둘 이상의 결과 집합을 반환 하는 문을 실행 하는 경우 사용할 수 있습니다는 [실행](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드는 SQLServerStatement 클래스를 반환 하므로 **부울** 여부를 나타내는 값은 반환 값에는 결과 집합 인지 업데이트 횟수는입니다.  
  
 Execute 메서드에서 반환 하는 경우 **true**, 실행 된 문 하나 이상의 결과 집합을 반환 했습니다. 첫 번째 결과 집합 getResultSet 메서드를 호출 하 여 액세스할 수 있습니다. 추가 결과 집합이 사용할 수 있는 경우 호출할 수 있습니다를 확인 하는 [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) 반환 하는 **부울** 값 **true** 추가 결과 집합이 있는 경우. 더 많은 결과 집합을 사용할 수 있으면 모든 결과 집합 처리 될 때까지 과정을 계속 getResultSet 메서드 액세스를 다시 호출할 수 있습니다. GetMoreResults 메서드를 반환 하는 경우 **false**는 더 많은 결과가 없습니다. 프로세스를 설정 합니다.  
  
 Execute 메서드에서 반환 하는 경우 **false**, 실행 된 문 호출 하 여 검색할 수는 업데이트 횟수 값을 반환 했습니다는 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 메서드.  
  
> [!NOTE]  
>  업데이트 횟수에 대 한 자세한 내용은 참조 [저장 프로시저를 사용 하 여 업데이트 횟수로](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)합니다.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스에는 함수에 전달 하 고 SQL 문을 생성 두 개의 결과 집합을 반환 하 실행 시:  
  
 [!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]  
  
 이 경우 반환된 결과 집합 수는 두 개로 알려져 있습니다. 하지만 저장 프로시저를 호출할 때와 같이 반환되는 결과 집합의 개수를 알 수 없는 경우 결과 집합을 모두 처리하도록 코드를 작성합니다. 업데이트 값과 함께 다중 결과 집합을 반환 하는 저장된 프로시저 호출 예를 보려면 [복잡 한 문을 처리](../../connect/jdbc/handling-complex-statements.md)합니다.  
  
> [!NOTE]  
>  SQLServerStatement 클래스의 getMoreResults 메서드를 호출 하면 이전에 반환된 된 결과 집합은 암시적으로 닫힙니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
