---
title: 매개 변수가 있는 SQL 문 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7b8b3f8b387345d91451c726b7f74a5685913f6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026654"
---
# <a name="using-an-sql-statement-with-parameters"></a>매개 변수가 있는 SQL 문 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

입력 매개 변수가 있는 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터 작업을 수행하려면 [SQLServerPreparedStatement](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) 클래스의 [executeQuery](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 메서드를 사용하여 요청한 데이터가 포함될 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)을 반환합니다. 이렇게 하려면 먼저 [SQLServerConnection](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) 클래스의 [prepareStatement](../../connect/jdbc/reference/sqlserverconnection-class.md) 메서드를 사용하여 SQLServerPreparedStatement 개체를 만들어야 합니다.

SQL 문을 생성할 때 물음표(?)를 사용하여 입력 매개 변수를 지정하면 SQL 문으로 전달될 매개 변수 값에 대한 자리 표시자로 사용됩니다. 매개 변수에 값을 지정하려면 SQLServerPreparedStatement 클래스의 setter 메서드 중 하나를 사용합니다. 사용하는 setter 메서드는 SQL 문에 전달할 값의 데이터 형식에 따라 결정됩니다.

setter 메서드에 값을 전달할 때는 SQL 문에 사용할 실제 값은 물론 SQL 문에서 해당 매개 변수의 서수 위치도 지정해야 합니다. 예를 들어 SQL 문에 단일 매개 변수가 포함되어 있는 경우 서수 값은 1이 됩니다. 명령문에 두 개의 매개 변수가 포함된 경우 첫 번째 서수 값은 1이고 두 번째 서수 값은 2가 됩니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, SQL의 준비된 명령문을 생성하여 단일 String 매개 변수 값으로 실행한 다음, 결과 집합에서 결과를 읽습니다.

[!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]

## <a name="see-also"></a>참고 항목

[SQL이 있는 문 사용](../../connect/jdbc/using-statements-with-sql.md)
