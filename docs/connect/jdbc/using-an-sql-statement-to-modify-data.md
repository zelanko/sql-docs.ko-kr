---
title: 데이터를 수정 하는 SQL 문을 사용 하 여 | Microsoft Docs
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
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d399da05226cb05506ad62cee3128a4a42aa0e6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-an-sql-statement-to-modify-data"></a>SQL 문을 사용하여 데이터 수정
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  에 포함 된 데이터를 수정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스는 SQL 문을 사용 하 여 사용할 수 있습니다는 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다. ExecuteUpdate 메서드는 처리를 위해 데이터베이스에는 SQL 문을 전달 되며 영향을 받는 행의 수를 나타내는 값을 반환 합니다.  
  
 이 수행 하려면 먼저 만들어야 합니다 SQLServerStatement 개체를 사용 하 여는 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스에 전달 함수, 테이블에 새 데이터를 추가 하는 SQL 문을 생성 하 고 다음 문을 실행 하 고 반환 값을 표시 합니다.  
  
 [!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]  
  
> [!NOTE]  
>  데이터를 수정 하려면 매개 변수를 포함 하는 SQL 문을 사용 해야 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스를 사용할지는 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) 의 메서드는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스입니다.  
>   
>  데이터를 삽입하려는 열에 공백 같은 특수 문자가 포함되어 있으면 기본값인 경우라도 삽입할 값을 제공해야 합니다. 그렇지 않으면 삽입 작업이 실패합니다.  
>   
>  JDBC 드라이버가 발생 가능성이 있는 모든 트리거가 반환한 업데이트 횟수를 포함하여 모든 업데이트 횟수를 반환하게 하려면 lastUpdateCount 연결 문자열 속성을 "false"로 설정합니다. LastUpdateCount 속성이 사용에 대 한 자세한 내용은 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)  
  
  
