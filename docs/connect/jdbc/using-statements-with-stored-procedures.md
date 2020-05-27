---
title: 저장 프로시저가 있는 문 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7fe07352ff1bcda9dd3ff3e77a6b879e592235a6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69025859"
---
# <a name="using-statements-with-stored-procedures"></a>저장 프로시저가 있는 문 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

저장 프로시저는 다른 프로그래밍 언어의 프로시저와 유사한 데이터베이스 프로시저이며, 데이터베이스 내에 들어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하거나 CLR(공용 언어 런타임) 및 Visual Basic 또는 C# 같은 Visual Studio 프로그래밍 언어 중 하나를 사용하여 저장 프로시저를 만들 수 있습니다. 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 다음을 수행할 수 있습니다.  
  
- 입력 매개 변수를 받아 여러 값을 출력 매개 변수의 형태로 호출하는 프로시저 또는 일괄 처리에 반환합니다.  
  
- 다른 프로시저 호출을 비롯하여 데이터베이스에서 작업을 수행하는 프로그래밍 문이 포함되어 있습니다.  
  
- 호출하는 프로시저 또는 일괄 처리에 상태 값을 반환하여 성공 또는 실패 및 실패 원인을 나타냅니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "저장 프로시저 이해"를 참조하세요.  
  
저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터에 대한 작업을 수행할 수 있도록 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 제공합니다. 어떤 클래스를 사용할지는 저장 프로시저의 입력 또는 출력 매개 변수 필요성 여부에 따라 달라집니다. 저장 프로시저가 입력 또는 출력 매개 변수가 필요하지 않은 경우 SQLServerStatement 클래스를 사용할 수 있으며, 저장 프로시저가 여러 번 호출되거나 입력 매개 변수만을 필요로 하는 경우에는 SQLServerPreparedStatement 클래스를 사용할 수 있습니다. 저장 프로시저에 입력 매개 변수와 출력 매개 변수가 모두 필요한 경우에는 SQLServerCallableStatement 클래스를 사용해야 합니다. 저장 프로시저에 출력 매개 변수만 필요한 경우에는 SQLServerCallableStatement 클래스 사용 오버헤드가 필요합니다.  
  
> [!NOTE]  
> 저장 프로시저는 업데이트 횟수 및 여러 결과 집합을 반환할 수도 있습니다. 자세한 내용은 [업데이트 횟수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) 및 [다중 결과 집합 사용](../../connect/jdbc/using-multiple-result-sets.md)을 참조하세요.  
  
JDBC 드라이버를 사용하여 매개 변수가 포함된 저장 프로시저를 호출하는 경우에는`call` SQL 이스케이프 시퀀스와 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 메서드를 함께 사용해야 합니다. `call` 이스케이프 시퀀스의 전체 구문은 다음과 같습니다.  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
> `call` 및 기타 SQL 이스케이프 시퀀스에 대한 자세한 내용은 [SQL 이스케이프 시퀀스 사용](../../connect/jdbc/using-sql-escape-sequences.md)을 참조하세요.  
  
이 섹션의 항목에서는 JDBC 드라이버 및 `call` SQL 이스케이프 시퀀스를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저를 호출하는 방법에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[매개 변수가 없는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|JDBC 드라이버를 사용하여 입력 또는 출력 매개 변수가 없는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[입력 매개 변수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|JDBC 드라이버를 사용하여 입력 매개 변수가 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[출력 매개 변수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|JDBC 드라이버를 사용하여 출력 매개 변수가 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[반환 상태가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|JDBC 드라이버를 사용하여 반환 상태 값이 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
|[업데이트 횟수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|JDBC 드라이버를 사용하여 업데이트 횟수가 있는 저장 프로시저를 실행하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
