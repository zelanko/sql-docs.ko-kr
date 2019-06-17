---
title: SQL 문을 사용 하 여 데이터 수정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2da0381f06e5092a7bcdb056d88df1160486ce0f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790240"
---
# <a name="using-an-sql-statement-to-modify-data"></a>SQL 문을 사용하여 데이터 수정

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 포함된 데이터를 수정하려면 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 메서드를 사용합니다. executeUpdate 메서드는 SQL 문을 데이터베이스로 전달하여 처리한 다음, 영향을 받은 행 수를 나타내는 값을 반환합니다.

이렇게 하려면 먼저 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 메서드를 사용하여 SQLServerStatement 개체를 만들어야 합니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, 테이블에 새 데이터를 추가하는 SQL 문을 생성한 다음, 해당 문을 실행하고 반환 값을 표시합니다.

[!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]

> [!NOTE]  
> 매개 변수가 있는 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 수정해야 하는 경우 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스의 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) 메서드를 사용해야 합니다.
>
> 데이터를 삽입하려는 열에 공백 같은 특수 문자가 포함되어 있으면 기본값인 경우라도 삽입할 값을 제공해야 합니다. 그렇지 않으면 삽입 작업이 실패합니다.
>
> JDBC 드라이버가 발생 가능성이 있는 모든 트리거가 반환한 업데이트 횟수를 포함하여 모든 업데이트 횟수를 반환하게 하려면 lastUpdateCount 연결 문자열 속성을 "false"로 설정합니다. LastUpdateCount 속성이 사용에 대 한 자세한 내용은 참조 하세요. [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)합니다.

## <a name="see-also"></a>참고 항목

[SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)
