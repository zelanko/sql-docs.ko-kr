---
title: SQL이 있는 문 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17e6253d0ff1f4fa9a26d97772fb9f7ff2890221
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923973"
---
# <a name="using-statements-with-sql"></a>SQL이 있는 문 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 인라인 SQL 문을 사용하여 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 데이터베이스의 데이터에 대한 작업을 수행하는 경우 다양한 클래스를 사용할 수 있습니다. 어떤 클래스를 사용할지는 실행하려는 SQL 문의 형식에 따라 달라집니다.  
  
SQL 문에 입력 매개 변수가 없는 경우 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스를 사용하고, 입력 매개 변수가 있는 경우 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스를 사용합니다.  
  
> [!NOTE]  
> 입력 및 출력 매개 변수가 모두 있는 SQL 문을 사용해야 하는 경우 저장 프로시저로 구현하고 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 사용하여 호출해야 합니다. 저장 프로시저를 사용에 대한 자세한 내용은 [저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)을 참조하세요.  
  
다음 섹션에서는 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 데이터 작업을 수행하는 여러 시나리오에 대해 설명합니다.  

## <a name="in-this-section"></a>섹션 내용  

| 항목                                                                                                                        | Description                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [매개 변수가 없는 SQL 문 사용](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | 매개 변수가 없는 SQL 문 사용 방법을 설명합니다.   |
| [매개 변수가 있는 SQL 문 사용](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | 매개 변수가 있는 SQL 문 사용 방법을 설명합니다.      |
| [SQL 문을 사용하여 데이터베이스 개체 수정](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | SQL 문을 사용하여 데이터베이스의 개체를 수정하는 방법을 설명합니다.   |
| [SQL 문을 사용하여 데이터 수정](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | SQL 문을 사용하여 데이터베이스의 데이터를 수정하는 방법을 설명합니다. |
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
