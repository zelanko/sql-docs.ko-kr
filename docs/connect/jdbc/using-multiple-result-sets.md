---
title: 여러 결과 집합 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f4b5232a71eaaf44fb9896d73b6ef63c7bf48c5f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798621"
---
# <a name="using-multiple-result-sets"></a>다중 결과 집합 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

둘 이상의 결과 집합을 반환하는 인라인 SQL 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저를 사용하는 경우 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 반환된 각 데이터 집합을 검색할 수 있도록 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스에 [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 메서드를 제공합니다. 또한 결과 집합을 둘 이상 반환하는 문을 실행하는 경우에는 SQLServerStatement 클래스의 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 사용합니다. 이는 반환된 값이 결과 집합인지 업데이트 횟수인지를 나타내는 **부울** 값을 반환합니다.

execute 메서드가 **true**를 반환하면 실행한 명령문은 하나 이상의 결과 집합을 반환합니다. getResultSet 메서드를 호출하면 첫 번째 결과 집합에 액세스할 수 있습니다. 추가 결과 집합이 있는지 확인하려면 추가 결과 집합이 있을 때 **부울** 값 **true**를 반환하는 [getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) 메서드를 호출합니다. 추가 결과 집합이 있는 경우 다시 getResultSet 메서드를 호출하여 액세스할 수 있으며 모든 결과 집합을 처리할 때까지 프로세스를 계속할 수 있습니다. GetMoreResults 메서드를 반환 하는 경우 **false**, 가지 자세한 결과가 없습니다. 프로세스를 설정 합니다.

execute 메서드가 **false**를 반환하면 실행한 명령문은 업데이트 횟수 값을 반환하며, 이 값은 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 메서드를 호출하여 검색할 수 있습니다.

> [!NOTE]  
> 업데이트 횟수에 대 한 자세한 내용은 참조 하세요. [업데이트 횟수가 있는 저장 프로시저를 사용 하 여](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)입니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대한 열린 연결을 함수에 전달하고, 실행 시 두 개의 결과 집합을 반환하는 SQL 문을 생성합니다.

[!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]

이 경우 반환된 결과 집합 수는 두 개로 알려져 있습니다. 하지만 저장 프로시저를 호출할 때와 같이 반환되는 결과 집합의 개수를 알 수 없는 경우 결과 집합을 모두 처리하도록 코드를 작성합니다. 업데이트 값과 함께 다중 결과 집합을 반환하는 저장 프로시저 호출 예를 보려면 [복잡한 명령문 처리](../../connect/jdbc/handling-complex-statements.md)를 참조하세요.

> [!NOTE]  
> SQLServerStatement 클래스의 getMoreResults 메서드 호출을 수행 하면 이전에 반환된 된 결과 집합은 암시적으로 닫힙니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
