---
title: RESTORE DATABASE(병렬 데이터 웨어하우스) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ed7e6aeb0630a20ee39d512fc17dfe24040737f2
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33702517"
---
# <a name="restore-database-parallel-data-warehouse"></a>RESTORE DATABASE(병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  데이터베이스 백업에서 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스로 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 사용자 데이터베이스를 복원합니다. 데이터베이스는 이전에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][BACKUP DATABASE&#40;병렬 데이터 웨어하우스&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md) 명령으로 만든 백업에서 복원됩니다. 백업 및 복원 작업을 사용하여 재해 복구 계획을 작성하거나 한 어플라이언스에서 다른 어플라이언스로 데이터베이스를 이동합니다.  
  
> [!NOTE]  
>  master 복원에는 어플라이언스 로그인 정보 복원이 포함됩니다. master를 복원하려면 **Configuration Manager** 도구의 [master 데이터베이스 복원&#40;Transact-SQL&#41; ](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) 페이지를 사용합니다. 제어 노드에 액세스할 수 있는 관리자가 이 작업을 수행할 수 있습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 백업에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에 있는 “백업 및 복원”을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
      Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>인수  
 RESTORE DATABASE *database_name*  
 사용자 데이터베이스를 *database_name*이라는 데이터베이스로 복원하도록 지정합니다. 복원된 데이터베이스 이름은 백업했던 원본 데이터베이스와 다를 수 있습니다. *database_name*은 대상 어플라이언스에 데이터베이스로 이미 존재할 수 없습니다. 허용된 데이터베이스 이름에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]의 “개체 명명 규칙”을 참조하세요.  
  
 사용자 데이터베이스를 복원하면 전체 데이터베이스 백업을 복원한 다음, 선택적으로 차등 백업을 어플라이언스에 복원합니다. 사용자 데이터베이스 복원에는 데이터베이스 사용자 및 데이터베이스 역할이 포함됩니다.  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]가 백업 파일을 복원할 네트워크 경로 및 디렉터리입니다. 예: FROM DISK = ‘\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup’.  
  
 *backup_directory*  
 전체 또는 차등 백업이 포함된 디렉터리의 이름을 지정합니다. 예를 들어 전체 또는 차등 백업에서 RESTORE HEADERONLY 작업을 수행할 수 있습니다.  
  
 *full_backup_directory*  
 전체 백업이 포함된 디렉터리의 이름을 지정합니다.  
  
 *differential_backup_directory*  
 차등 백업이 포함된 디렉터리의 이름을 지정합니다.  
  
-   경로 및 백업 디렉터리는 이미 존재해야 하며 정규화된 UNC(범용 명명 규칙) 경로로 지정해야 합니다.  
  
-   백업 디렉터리 경로는 로컬 경로일 수 없으며 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스 노드의 위치일 수 없습니다.  
  
-   UNC 경로 및 백업 디렉터리 이름의 최대 길이는 200자입니다.  
  
-   서버 또는 호스트는 IP 주소로 지정해야 합니다.  
  
 RESTORE HEADERONLY  
 한 명의 사용자 데이터베이스 백업에 대한 헤더 정보만 반환하도록 지정합니다. 다른 필드 간에 헤더의 텍스트 설명 및 백업 이름을 포함합니다. 백업 이름은 백업 파일을 저장하는 디렉터리의 이름과 같을 필요는 없습니다.  
  
 RESTORE HEADERONLY 결과는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 결과 뒤에 패턴화됩니다. 결과에는 50개 이상의 열이 있으며 모두 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 사용되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 결과의 열에 대한 설명은 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 **CREATE ANY DATABASE** 권한이 필요합니다.  
  
 백업 디렉터리에 액세스하고 읽을 수 있는 권한이 있는 Windows 계정이 필요합니다. 또한 Windows 계정 이름 및 암호를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 저장해야 합니다.  
  
1.  자격 증명이 이미 있는지 확인하려면 [sys.dm_pdw_network_credentials&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)를 사용합니다.  
  
2.  자격 증명을 추가하거나 업데이트하려면 [sp_pdw_add_network_credentials&#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)를 사용합니다.  
  
3.  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 자격 증명을 제거하려면 [sp_pdw_remove_network_credentials&#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)를 사용합니다.  
  
## <a name="error-handling"></a>오류 처리  
 RESTORE DATABASE 명령은 다음과 같은 조건에서 오류를 발생시킵니다.  
  
-   저장할 데이터베이스의 이름이 이미 대상 어플라이언스에 있습니다. 이를 방지하려면 고유한 데이터베이스 이름을 선택하거나 복원을 실행하기 전에 기존 데이터베이스를 삭제합니다.  
  
-   백업 디렉터리에 백업 파일의 잘못된 집합이 있습니다.  
  
-   로그인 권한이 데이터베이스를 복원하기에 충분하지 않습니다.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 백업 파일이 저장될 네트워크 위치에 대한 올바른 사용 권한이 없습니다.  
  
-   백업 디렉터리에 대한 네트워크 위치가 존재하지 않거나 사용할 수 없습니다.  
  
-   계산 노드 또는 제어 노드에 충분한 디스크 공간이 없습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 복원을 시작하기 전에 어플라이언스에 충분한 디스크 공간이 있는지를 확인하지 않습니다. 따라서 RESTORE DATABASE 문을 실행하는 동안 디스크 공간 부족 오류가 발생할 가능성이 있습니다. 디스크 공간이 부족하면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 복원을 롤백합니다.  
  
-   데이터베이스를 복원하는 대상 어플라이언스는 데이터베이스를 백업한 원본 어플라이언스보다 계산 노드가 더 적습니다.  
  
-   데이터베이스 복원은 트랜잭션 내에서 시도됩니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 데이터베이스 복원의 성공 여부를 추적합니다. 차등 데이터베이스 백업을 복원하기 전에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 성공적으로 전체 데이터베이스 복원이 완료되었는지 확인합니다.  
  
 복원 후 사용자 데이터베이스는 데이터베이스 호환성 수준 120을 갖게 됩니다. 이는 원래 호환성 수준에 관계 없이 모든 데이터베이스에 마찬가지입니다.  
  
 **계산 노드 수가 더 많은 어플라이언스에 복원**  
재배포하면 트랜잭션 로그가 증가하므로 작은 어플라이언스에서 큰 어플라이언스로 데이터베이스를 복원한 후 [DBCC SHRINKLOG(Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)를 실행합니다.  

계산 노드 수가 많은 어플라이언스로 백업을 복원하면 계산 노드 수에 비례하여 할당된 데이터베이스 크기가 커집니다.  
  
예를 들어 60GB의 데이터베이스를 2개 노드 어플라이언스(노드당 30GB)에서 6개 노드 어플라이언스로 복원하는 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 6개 노드 어플라이언스에서 180GB 데이터베이스(노드당 30GB의 6개 노드)를 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 처음에 데이터베이스를 원본 구성에 일치하도록 2개 노드로 복원한 다음, 6개 노드 모두에 데이터를 다시 배포합니다.  
  
 재배포 후 각 계산 노드는 더 작은 원본 어플라이언스에서 각 계산 노드에 비해 더 적은 실제 데이터와 더 많은 여유 공간을 포함하게 됩니다. 데이터베이스에 더 많은 데이터를 추가하려면 추가 공간을 사용합니다. 복원된 데이터베이스 크기가 필요한 것보다 더 큰 경우 [ALTER DATABASE&#40;병렬 데이터 웨어하우스&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)를 사용하여 데이터베이스 파일 크기를 축소할 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 이러한 제한 사항의 경우 원본 어플라이언스는 데이터베이스 백업을 만든 어플라이언스이며, 대상 어플라이언스는 데이터베이스를 복원할 어플라이언스입니다.  
  
 데이터베이스 복원은 통계를 자동으로 빌드하지 않습니다.  
  
 하나의 RESTORE DATABASE 또는 BACKUP DATABASE 문은 언제든지 어플라이언스에서 실행할 수 있습니다. 동시에 여러 백업 및 복원 명령문이 제출되면 어플라이언스는 이를 큐에 배치하고 한 번에 하나씩 처리합니다.  
  
 데이터베이스 백업은 원본 어플라이언스에 비해 계산 노드가 동일하거나 더 많은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 대상 어플라이언스에 복원할 수 있습니다. 대상 어플라이언스는 원본 어플라이언스보다 계산 노드가 더 많아야 합니다.  
  
 SQL Server 2012 PDW 하드웨어가 있는 어플라이언스에서 만든 백업을 SQL Server 2008 R2 하드웨어가 있는 어플라이언스에 복원할 수 없습니다. 처음에 SQL Server 2008 R2 PDW 하드웨어와 함께 어플라이언스를 구매했고 현재 SQL Server 2012 PDW 소프트웨어를 실행하는 경우에도 마찬가지입니다.  
  
## <a name="locking"></a>잠금  
 DATABASE 개체에서 배타적 잠금을 사용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-restore-examples"></a>1. 간단한 RESTORE 예  
 다음 예에서는 전체 백업을 `SalesInvoices2013` 데이터베이스에 복원합니다. 백업 파일은 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 디렉터리에 저장됩니다. SalesInvoices2013 데이터베이스는 대상 어플라이언스에 이미 존재할 수 없으며, 그렇지 않으면 이 명령은 오류가 발생하여 실패합니다.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>2. 전체 및 차등 백업 복원  
 다음 예에서는 SalesInvoices2013 데이터베이스에 전체 및 차등 백업을 차례로 복원합니다.  
  
 데이터베이스의 전체 백업은 ‘\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full’ 디렉터리에 저장되는 전체 백업에서 복원됩니다. 복원이 성공적으로 완료되면 차등 백업이 SalesInvoices2013 데이터베이스에 복원됩니다.  차등 백업은 ‘\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff’ 디렉터리에 저장됩니다.  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>3. 백업 헤더 복원  
 이 예제는 데이터베이스 백업 ‘\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full’에 대한 헤더 정보를 복원합니다. 명령은 Invoices2013Full 백업에 대한 정보에서 하나의 행에 발생합니다.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 헤더 정보를 사용하여 백업 복원을 시도하기 전에 백업의 콘텐츠를 확인하거나 대상 복원 어플라이언스가 원본 백업 어플라이언스와 호환되는지 확인할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP DATABASE&#40;Parallel Data Warehouse&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
