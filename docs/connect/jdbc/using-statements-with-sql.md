---
title: SQL 문 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 743616c9a18704bdd91a0d44259d3c980dcc2c9d
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784470"
---
# <a name="using-statements-with-sql"></a>SQL이 있는 문 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 및 인라인 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터에 대한 작업을 수행하는 경우 다양한 클래스를 사용할 수 있습니다. 어떤 클래스를 사용할지는 실행하려는 SQL 문의 형식에 따라 달라집니다.  
  
SQL 문에 입력 매개 변수가 없는 경우 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스를 사용하고, 입력 매개 변수가 있는 경우 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스를 사용합니다.  
  
> [!NOTE]  
> 입력 및 출력 매개 변수가 모두 있는 SQL 문을 사용해야 하는 경우 저장 프로시저로 구현하고 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 사용하여 호출해야 합니다. 저장된 프로시저를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [저장 프로시저를 사용 하 여 문을 사용 하 여](../../connect/jdbc/using-statements-with-stored-procedures.md)입니다.  
  
다음 섹션에서는 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 데이터 작업을 수행하는 여러 시나리오에 대해 설명합니다.  

## <a name="in-this-section"></a>섹션 내용  

| 항목                                                                                                                        | 설명                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [매개 변수가 없는 SQL 문 사용](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | 매개 변수가 없는 SQL 문 사용 방법을 설명합니다.   |
| [매개 변수가 있는 SQL 문 사용](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | 매개 변수가 있는 SQL 문 사용 방법을 설명합니다.      |
| [SQL 문을 사용하여 데이터베이스 개체 수정](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | SQL 문을 사용하여 데이터베이스의 개체를 수정하는 방법을 설명합니다.   |
| [SQL 문을 사용하여 데이터 수정](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | SQL 문을 사용하여 데이터베이스의 데이터를 수정하는 방법을 설명합니다. |
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
