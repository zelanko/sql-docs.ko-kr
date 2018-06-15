---
title: 문 및 결과 집합 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14a6f86b503cf4c0f864a881479a37314c11d528
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852278"
---
# <a name="working-with-statements-and-result-sets"></a>문 및 결과 집합 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  작업을 할 때는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 및 문에 및 결과 집합 개체에서 제공 하는 성능 및 응용 프로그램의 안정성을 개선 하기 위해 사용할 수 있는 방법은 여러 가지가 있습니다.  
  
## <a name="use-the-appropriate-statement-object"></a>알맞은 문 개체 사용  
 하나를 사용 하면 JDBC 드라이버는 Statement 개체를 같은 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), 또는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체 작업에 대 한 적절 한 개체를 사용 하 고 있는지 확인 합니다.  
  
-   OUT 매개 변수 않아도 SQLServerCallableStatement 개체를 사용할 필요가 없습니다. SQLServerStatement 또는 SQLServerPreparedStatement 개체를 대신 사용 합니다.  
  
-   OUT 매개 변수 또는 두 번 이상 문을 실행 하지 않으려는 하거나 없는 경우 SQLServerCallableStatement 또는 SQLServerPreparedStatement 개체를 사용할 필요가 없습니다. 대신, SQLServerStatement 개체를 사용 합니다.  
  
## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>결과 집합 개체에 알맞은 동시성 사용  
 실제로 결과를 업데이트할 의도가 없다면 결과 집합을 생성하는 문을 만들 때 업데이트 가능한 동시성이 필요치 않습니다. 기본적인 정방향 전용, 읽기 전용 커서 모델이 작은 결과 집합을 읽는 데에는 가장 효율적입니다.  
  
## <a name="limit-the-size-of-your-result-sets"></a>결과 집합 크기 제한  
 사용 하는 것이 좋습니다는 [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) 잠재적으로 큰 결과 집합에서 반환 된 행의 수를 제한 하려면 메서드 (또는 SET ROWCOUNT 또는 SELECT TOP N SQL 구문). 큰 결과 집합을 처리해야 하는 경우 연결 문자열 속성 responseBuffering을 기본 모드인 adaptive로 설정하여 선택 응답 버퍼링을 사용해 보십시오. 이 방식을 사용하면 응용 프로그램에서 서버측 커서를 사용하지 않고 큰 결과 집합을 처리할 수 있으며 응용 프로그램 메모리 사용도 최소화할 수 있습니다. 자세한 내용은 참조 [선택 버퍼링 사용 하 여](../../connect/jdbc/using-adaptive-buffering.md)합니다.  
  
## <a name="use-the-appropriate-fetch-size"></a>알맞은 반입 크기 사용  
 읽기 전용 서버 커서의 경우 드라이버에 사용되는 메모리 양과 서버와의 왕복 횟수 사이에 역관계가 성립합니다. 업데이트 가능 서버 커서의 경우 반입 크기 역시 서버의 변경 내용과 동시성에 대한 결과 집합의 중요도에 영향을 미칩니다. 명시적 될 때까지 현재 반입 버퍼 내에서 행에 대 한 업데이트 표시 되지 않습니다 [refreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md) 메서드를 발급 하거나 커서가 반입 버퍼를 떠날 때까지 합니다. 반입 버퍼가 크면 성능이 높아지지만(서버 왕복 이동은 적음) CONCUR_SS_SCROLL_LOCKS (1009)를 사용한 경우 서버의 변경 내용에 따른 중요도가 떨어지고 동시성도 감소합니다. 변경 내용에 따른 중요도를 최대로 설정하려면 반입 크기 1을 사용합니다. 하지만 이렇게 하면 반입되는 모든 행에 대해 서버로의 왕복 이동이 발생합니다.  
  
## <a name="use-streams-for-large-in-parameters"></a>큰 입력 매개 변수에 대한 스트림 사용  
 점점 구체화되는 스트림 또는 BLOB와 CLOB를 사용하여 큰 열 값의 업데이트나 큰 입력 매개 변수 전송을 처리합니다. JDBC 드라이버에서는 여러 번의 왕복 이동으로 서버까지 이들을 "청크" 처리하므로 메모리에 알맞은 크기 이상의 값을 설정하고 업데이트할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
