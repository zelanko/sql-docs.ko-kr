---
title: "분리 및 연결을 사용하여 데이터베이스 이동(Transact-SQL) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database attaching [SQL Server]
- moving databases [SQL Server]
- database detaching [SQL Server]
- relocating databases [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 6732a431-cdef-4f1e-9262-4ac3b77c275e
caps.latest.revision: 47
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4604a9d4da9360607e31d31b3f160bc0bff2eac
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="move-a-database-using-detach-and-attach-transact-sql"></a>분리 및 연결을 사용하여 데이터베이스 이동(Transact-SQL)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 분리된 데이터베이스를 다른 위치로 이동하고 동일한 서버 인스턴스나 다른 서버 인스턴스에 다시 연결하는 방법에 대해 설명합니다. 하지만 데이터베이스를 이동할 때는 분리 및 연결 작업 대신 계획된 ALTER DATABASE 재배치 프로시저를 사용하는 것이 좋습니다. 자세한 내용은 [Move User Databases](../../relational-databases/databases/move-user-databases.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  알 수 없거나 신뢰할 수 없는 출처의 데이터베이스는 연결 또는 복원하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.  
  
## <a name="procedure"></a>절차  
  
#### <a name="to-move-a-database-by-using-detach-and-attach"></a>분리 및 연결 작업을 사용하여 데이터베이스를 이동하려면  
  
1.  데이터베이스를 분리합니다. 자세한 내용은 [데이터베이스 분리](../../relational-databases/databases/detach-a-database.md)를 참조하세요.  
  
2.  Windows 탐색기나 Windows 명령 프롬프트 창에서 분리된 데이터베이스 파일과 로그 파일을 새 위치로 이동합니다.  
  
    > [!NOTE]  
    >  전자 메일로 보낼 수 있을 정도로 파일 크기가 작으면 한 개의 파일로 구성된 데이터베이스를 이동하는 데 전자 메일을 사용할 수 있습니다.  
  
     새 로그 파일을 작성할 경우에도 로그 파일을 이동해야 합니다. 경우에 따라 데이터베이스를 다시 연결하려면 기존 로그 파일이 필요합니다. 따라서 데이터베이스가 분리된 로그 파일 없이도 성공적으로 연결될 때까지 모든 분리된 로그 파일을 항상 보존하세요.  
  
    > [!NOTE]  
    >  로그 파일을 지정하지 않고 데이터베이스를 연결할 경우 연결 작업은 원래 위치에서 로그 파일을 검색합니다. 원래 위치에 로그 복사본이 있으면 해당 복사본이 연결됩니다. 원래 로그 파일을 사용하지 않으려면 새 로그 파일의 경로를 지정하거나 로그 파일의 원본을 새 위치로 복사한 후 제거합니다.  
  
3.  복사된 파일을 연결합니다. 자세한 내용은 [Attach a Database](../../relational-databases/databases/attach-a-database.md)을(를) 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 라고 하는 `MyAdventureWorks`데이터베이스의 복사본을 만듭니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 연결한 서버 인스턴스에 연결된 쿼리 편집기 창에서 실행됩니다.  
  
1.  다음 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 문을 실행하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터베이스를 분리합니다.  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'AdventureWorks2012';  
    GO  
    ```  
  
2.  선택한 방법을 사용하여 데이터베이스 파일(AdventureWorks208R2_Data.mdf 및 AdventureWorks208R2_log)을 각각 C:\MySQLServer\AdventureWorks208R2_Data.mdf 및 C:\MySQLServer\AdventureWorks208R2_Log.ldf로 복사합니다.  
  
    > [!IMPORTANT]  
    >  프로덕션 데이터베이스의 경우 데이터베이스와 트랜잭션 로그를 별도의 디스크에 저장합니다.  
  
     네트워크를 통해 원격 컴퓨터의 디스크로 파일을 복사하려면 원격 위치의 UNC(Universal Naming Convention) 이름을 사용합니다. UNC 이름의 형식은 **\\\\***Servername***\\***Sharename***\\***Path***\\***Filename*입니다. 로컬 하드 디스크에 파일을 쓸 경우 원격 디스크의 파일을 읽거나 파일에 쓰는 데 필요한 해당 권한은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 사용하는 사용자 계정에게 부여되어야 합니다.  
  
3.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 이동된 데이터베이스와 필요에 따라 해당 로그를 연결합니다.  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Data.mdf'),  
        (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Log.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새로 연결되는 데이터베이스는 개체 탐색기에 즉시 표시되지 않습니다. 데이터베이스를 보려면 개체 탐색기에서 **보기** , **새로 고침**을 차례로 클릭합니다. 개체 탐색기에서 **데이터베이스** 노드가 확장될 때 새로 연결된 데이터베이스가 데이터베이스 목록에 나타납니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

