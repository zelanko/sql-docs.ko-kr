---
title: Sql 문을 사용 하 여 | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 242b7ca6f483b65e054b43ef0fa370b57bd3f272
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-statements-with-sql"></a>SQL이 있는 문 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터로 작업할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용 하 여 데이터베이스의 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 및 인라인 SQL 문을 사용할 수 있는 다양 한 클래스입니다. 어떤 클래스를 사용할지는 실행하려는 SQL 문의 형식에 따라 달라집니다.  
  
 SQL 문의 매개 변수가 없는 사용 하 여는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스 같지만 사용 하 여 매개 변수에서 포함 하는 경우에 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스입니다.  
  
> [!NOTE]  
>  변수가 모두 있는 SQL 문을 사용 해야 하 고 OUT 매개 변수를 저장된 프로시저로 구현 및 사용 하 여 호출 해야 하는 경우는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스입니다. 저장된 프로시저를 사용 하는 방법에 대 한 자세한 내용은 참조 [저장 프로시저와 함께 Using 문을](../../connect/jdbc/using-statements-with-stored-procedures.md)합니다.  
  
 다음 섹션에서는 데이터를 사용 하는 것에 대 한 다양 한 시나리오를 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL 문을 사용 하 여 데이터베이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[매개 변수가 없는 SQL 문 사용](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|매개 변수가 없는 SQL 문 사용 방법을 설명합니다.|  
|[매개 변수가 있는 SQL 문 사용](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|매개 변수가 있는 SQL 문 사용 방법을 설명합니다.|  
|[SQL 문을 사용하여 데이터베이스 개체 수정](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|SQL 문을 사용하여 데이터베이스의 개체를 수정하는 방법을 설명합니다.|  
|[SQL 문을 사용하여 데이터 수정](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|SQL 문을 사용하여 데이터베이스의 데이터를 수정하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
