---
title: SQL 문을 사용 하 여 데이터베이스 개체를 수정 하려면 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b126fb0b5a72688c1801cf8854d8035763c8245f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851498"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>SQL 문을 사용하여 데이터베이스 개체 수정
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  수정 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 사용할 수는 SQL 문을 사용 하 여 데이터베이스 개체는 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다. ExecuteUpdate 메서드는 처리를 위해 데이터베이스에는 SQL 문을 전달 되며 행이 없는 영향을 하기 때문에 0 값을 반환 합니다.  
  
 이 수행 하려면 먼저 만들어야 합니다 SQLServerStatement 개체를 사용 하 여는 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다.  
  
> [!NOTE]  
>  데이터베이스에서 개체를 수정하는 SQL 문은 DDL(데이터 정의 언어) 문이라고 합니다. DDL 문에는 CREATE TABLE, DROP TABLE, CREATE INDEX 및 DROP INDEX 등의 문이 있습니다. 지원 되는 DDL 문의 종류에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 되는 SQL 문을 생성, 데이터베이스에 간단한 테스트 테이블을 만듭니다는 다음 문을 실행 및 반환 값을 표시 합니다.  
  
 [!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)  
  
  
