---
title: SQL 문을 사용하여 데이터베이스 개체 수정 | Microsoft Docs
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
ms.openlocfilehash: a3386121432f918ef447f5d3ad1f4ff79a64c681
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662445"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>SQL 문을 사용하여 데이터베이스 개체 수정

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 개체를 수정하려면 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 메서드를 사용합니다. executeUpdate 메서드는 SQL 문을 데이터베이스에 전달하여 처리한 다음, 적용된 행이 없기 때문에 0 값을 반환합니다.

이렇게 하려면 먼저 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 메서드를 사용하여 SQLServerStatement 개체를 만들어야 합니다.

> [!NOTE]  
> 데이터베이스에서 개체를 수정하는 SQL 문은 DDL(데이터 정의 언어) 문이라고 합니다. 와 같은 이러한 include 문을 `CREATE TABLE`, `DROP TABLE`를 `CREATE INDEX`, 및 `DROP INDEX`합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서 지원하는 DDL 문의 형식에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서를 참조하세요.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, 데이터베이스에 간단한 테스트 테이블을 만드는 SQL 문을 생성한 다음, 해당 명령문을 실행하고 반환 값을 표시합니다.

[!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]

## <a name="see-also"></a>참고 항목

[SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)
