---
title: Stretch Database 비활성화 및 원격 데이터 다시 가져오기 | Microsoft 문서
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 791ead536a9e5582ddb06886b8003e598507b273
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="disable-stretch-database-and-bring-back-remote-data"></a>Stretch Database 비활성화 및 원격 데이터 다시 가져오기
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  테이블에서 Stretch Database를 사용하지 않으려면 SQL Server Management Studio 테이블에서 **스트레치** 를 선택합니다. 그리고 다음 옵션 중 하나를 선택합니다.  
  
-   **사용 안 함 | Azure에서 데이터 다시 가져오기**. Azure에서 테이블에 대한 원격 데이터를 SQL Server로 다시 복사한 후 테이블에서 스트레치 데이터베이스를 비활성화합니다. 이 작업으로 인해 데이터 전송 비용이 발생하며 이 작업은 취소할 수 없습니다.  
  
-   **사용 안 함 | Azure에 데이터 유지**. 테이블에서 스트레치 데이터베이스를 사용하지 않도록 설정합니다.  Azure에서 테이블에 대한 원격 데이터를 중단합니다.  
  
 또한, Transact-SQL을 사용하여 테이블 또는 데이터베이스에서 스트레치 데이터베이스를 사용하지 않을 수 있습니다.  
  
 테이블에서 Stretch Database를 비활성화하면 데이터 마이그레이션이 중단되고 쿼리 결과에 원격 테이블의 결과가 더 이상 포함되지 않습니다.  
  
 데이터 마이그레이션을 일시 중지하려면 [데이터 마이그레이션 일시 중지 및 다시 시작&#40;스트레치 데이터베이스&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
> [!NOTE]
> 테이블 또는 데이터베이스에서 Stretch Database를 비활성화하면 원격 개체가 삭제되지 않습니다. 원격 테이블 또는 원격 데이터베이스를 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 개체는 삭제할 때까지 Azure 비용이 계속해서 발생합니다. 자세한 내용은 [SQL Server 스트레치 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)를 참조하십시오.  
  
## <a name="disable-stretch-database-for-a-table"></a>테이블에서 스트레치 데이터베이스 비활성화  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-table"></a>SQL Server Management Studio를 사용하여 테이블에서 스트레치 데이터베이스를 비활성화  
  
1.  SQL Server Management Studio의 개체 탐색기에서 스트레치 데이터베이스를 비활성화하려는 테이블을 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **스트레치**를 선택한 후 다음 옵션 중 하나를 선택합니다.  
  
    -   **사용 안 함 | Azure에서 데이터 다시 가져오기**. Azure에서 테이블에 대한 원격 데이터를 SQL Server로 다시 복사한 후 테이블에서 스트레치 데이터베이스를 비활성화합니다. 이 명령은 취소할 수 없습니다.  
  
        > [!NOTE]
        > Azure에서 SQL Server로 원격 데이터를 다시 복사하면 데이터 전송 비용이 발생합니다. 자세한 내용은 [데이터 전송 가격 정보](https://azure.microsoft.com/pricing/details/data-transfers/)를 참조하십시오.  
  
         Azure에서 SQL Server로 모든 원격 데이터를 다시 복사한 후 테이블에서 스트레치가 비활성화됩니다.  
  
    -   **사용 안 함 | Azure에 데이터 유지**. 테이블에서 스트레치 데이터베이스를 사용하지 않도록 설정합니다.  Azure에서 테이블에 대한 원격 데이터를 중단합니다.  
  
    > [!NOTE]
    > 테이블에서 스트레치 데이터베이스를 비활성화하면 원격 개체 또는 원격 테이블이 삭제되지 않습니다. 원격 테이블을 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 테이블은 삭제할 때까지 Azure 비용이 계속해서 발생합니다. 자세한 내용은 [SQL Server 스트레치 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)를 참조하십시오.  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-table"></a>Transact-SQL을 사용하여 테이블에서 스트레치 데이터베이스 비활성화  
  
-   테이블에서 스트레치를 비활성화하고 Azure에서 SQL Server로 테이블에 대한 원격 데이터를 다시 복사하려면 다음 명령을 실행합니다. Azure에서 SQL Server로 모든 원격 데이터를 다시 복사한 후에는 스트레치가 테이블에 대해 비활성화됩니다.

    이 명령은 취소할 수 없습니다.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE]
    > Azure에서 SQL Server로 원격 데이터를 다시 복사하면 데이터 전송 비용이 발생합니다. 자세한 내용은 [데이터 전송 가격 정보](https://azure.microsoft.com/pricing/details/data-transfers/)를 참조하십시오.    
  
-   테이블에서 스트레치를 비활성화하고 원격 데이터를 중지하려면 다음 명령을 실행합니다.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE]
> 테이블에서 스트레치 데이터베이스를 비활성화하면 원격 개체 또는 원격 테이블이 삭제되지 않습니다. 원격 테이블을 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 테이블은 삭제할 때까지 Azure 비용이 계속해서 발생합니다. 자세한 내용은 [SQL Server 스트레치 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)를 참조하십시오.  
  
## <a name="disable-stretch-database-for-a-database"></a>데이터베이스에서 Stretch Database 비활성화  
 데이터베이스에서 개별적으로 스트레치가 활성화된 테이블에 대한 스트레치 데이터베이스를 비활성화한 후 데이터베이스에서 스트레치 데이터베이스를 비활성화할 수 있습니다.  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-database"></a>SQL Server Management Studio를 사용하여 데이터베이스에서 스트레치 데이터베이스 비활성화  
  
1.  SQL Server Management Studio의 개체 탐색기에서 스트레치 데이터베이스를 비활성화하려는 데이터베이스를 선택합니다.  
  
2.  마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **스트레치**를 선택하고 **사용 안 함**을 선택합니다.  
  
> [!NOTE]
> 데이터베이스에서 스트레치 데이터베이스를 비활성화하면 원격 데이터베이스가 삭제되지 않습니다. 원격 데이터베이스를 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 데이터베이스는 삭제할 때까지 Azure 비용이 계속해서 발생합니다. 자세한 내용은 [SQL Server 스트레치 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)를 참조하십시오.  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-database"></a>Transact-SQL을 사용하여 데이터베이스에서 스트레치 데이터베이스 비활성화  
 다음 명령을 실행합니다.  
  
```sql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE]
> 데이터베이스에서 스트레치 데이터베이스를 비활성화하면 원격 데이터베이스가 삭제되지 않습니다. 원격 데이터베이스를 삭제하려면 Azure 관리 포털을 사용하여 삭제해야 합니다. 원격 데이터베이스는 삭제할 때까지 Azure 비용이 계속해서 발생합니다. 자세한 내용은 [SQL Server 스트레치 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [데이터 마이그레이션 일시 중지 및 다시 시작&#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  
