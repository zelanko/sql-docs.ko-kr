---
title: 저장 프로시저와 문을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eef81eed0bafd9ea342bc483de0130dcb60a81f6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-statements-with-stored-procedures"></a>저장 프로시저가 있는 문 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  저장 프로시저는 다른 프로그래밍 언어의 프로시저와 유사한 데이터베이스 프로시저이며, 데이터베이스 내에 들어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 저장된 프로시저를 사용 하 여 만들 수 있습니다 [!INCLUDE[tsql](../../includes/tsql_md.md)], 또는 공용 언어 런타임 (CLR) 및 Visual Studio 중 하나를 사용 하 여 Visual Basic 또는 C# 등의 언어와 프로그래밍 합니다. 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 저장된 프로시저는 다음을 수행할 수 있습니다.  
  
-   입력 매개 변수를 받아 여러 값을 출력 매개 변수의 형태로 호출하는 프로시저 또는 일괄 처리에 반환합니다.  
  
-   다른 프로시저 호출을 비롯하여 데이터베이스에서 작업을 수행하는 프로그래밍 문이 포함되어 있습니다.  
  
-   호출하는 프로시저 또는 일괄 처리에 상태 값을 반환하여 성공 또는 실패 및 실패 원인을 나타냅니다.  
  
> [!NOTE]  
>  에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 저장된 프로시저의 "저장 프로시저 이해"를 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
 에 데이터로 작업 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 저장된 프로시저를 사용 하 여 데이터베이스의 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 제공는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), 및 [ SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스입니다. 어떤 클래스를 사용할지는 저장 프로시저의 입력 또는 출력 매개 변수 필요성 여부에 따라 달라집니다. SQLServerStatement 클래스; 저장된 프로시저에 필요 하지 않은 경우 또는 OUT 매개 변수를 사용할 수 있습니다. 저장된 프로시저가 여러 번 호출 하거나 매개 변수 에서만에서 필요한를 경우 SQLServerPreparedStatement 클래스를 사용할 수 있습니다. 저장된 프로시저 모두 필요로 하는 경우 및 OUT 매개 변수를 SQLServerCallableStatement 클래스를 사용 해야 합니다. 되었기만 저장된 프로시저에 필요한 경우 OUT 매개 변수는 SQLServerCallableStatement 클래스 사용 오버 헤드가 필요 합니다.  
  
> [!NOTE]  
>  저장 프로시저는 업데이트 횟수 및 여러 결과 집합을 반환할 수도 있습니다. 자세한 내용은 참조 [업데이트 횟수가 있는 저장 프로시저를 사용 하 여](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) 및 [여러 결과 집합을 사용 하 여](../../connect/jdbc/using-multiple-result-sets.md)합니다.  
  
 JDBC 드라이버를 사용 하 여 매개 변수가 있는 저장된 프로시저를 호출 하는 경우 사용 해야는 `call` 와 함께 SQL 이스케이프 시퀀스는 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다. 전체 구문은 `call` 이스케이프 시퀀스는 다음과 같습니다.  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  에 대 한 자세한 내용은 `call` 및 다른 SQL 이스케이프 시퀀스, 참조 [SQL 이스케이프 시퀀스를 사용 하 여](../../connect/jdbc/using-sql-escape-sequences.md)합니다.  
  
 이 섹션의 항목 호출할 수 있는 방법에 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC 드라이버를 사용 하 여 저장 프로시저 및 `call` SQL 이스케이프 시퀀스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[매개 변수가 없는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|JDBC 드라이버를 사용하여 입력 또는 출력 매개 변수가 없는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[입력 매개 변수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|JDBC 드라이버를 사용하여 입력 매개 변수가 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[출력 매개 변수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|JDBC 드라이버를 사용하여 출력 매개 변수가 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[반환 상태가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|JDBC 드라이버를 사용하여 반환 상태 값이 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[업데이트 횟수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|JDBC 드라이버를 사용하여 업데이트 횟수가 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
