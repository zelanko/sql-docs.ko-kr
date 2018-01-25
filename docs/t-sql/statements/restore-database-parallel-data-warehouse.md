---
title: "데이터베이스 복원 (병렬 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ba8aa12f38fce6ac00f88f0015008da25a59b88
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-database-parallel-data-warehouse"></a>(병렬 데이터 웨어하우스) 데이터베이스를 복원 합니다.
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  복원 된 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 사용자 데이터베이스에서 데이터베이스를 백업 하는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 기기입니다. 데이터베이스에서 이전에 만든 백업에서 복원 되는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [데이터베이스 백업 &#40; 병렬 데이터 웨어하우스 &#41; ](../../t-sql/statements/backup-database-parallel-data-warehouse.md) 명령입니다. 백업 하 고 복원 작업을 재해 복구 계획을 작성 하거나 다른 한 기기에서 데이터베이스를 이동 합니다.  
  
> [!NOTE]  
>  Master를 복원한 포함 어플라이언스에 로그인 정보를 복원 합니다. 사용 하 여 마스터 복원는 [master 데이터베이스 &#40; 복원 Transact SQL &#41; ](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) 페이지에 **Configuration Manager** 도구입니다. 에 제어 노드에 액세스할 수 있는 관리자가이 작업을 수행할 수 있습니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 백업, "백업 및 복원"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 데이터베이스 복원 *database_name*  
 사용자 데이터베이스 라는 데이터베이스를 복원 하려면 지정 *database_name*합니다. 복원된 된 데이터베이스에는 백업 했던 원본 데이터베이스와 다른 이름을 가질 수 있습니다. *a s e _* 대상 어플라이언스에 데이터베이스로 이미 있을 수 없습니다. 에 대 한 자세한 내용은 "개체 이름 지정 규칙"를 참조 데이터베이스의 이름에 허용 된 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 사용자 데이터베이스를 복원 합니다. 전체 데이터베이스 백업을 복원 하 고 기기에 필요에 따라 차등 백업에 복원 합니다. 사용자 데이터베이스의 복원을 복원 하는 데이터베이스 사용자 및 데이터베이스 역할을 포함 합니다.  
  
 디스크에서 = '\\\\*UNC_path*\\*backup_directory*'  
 네트워크 경로 및 디렉터리를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업 파일을 복원 합니다. 예를 들어 디스크 = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
 *backup_directory*  
 전체 또는 차등 백업이 포함 된 디렉터리의 이름을 지정 합니다. 예를 들어 전체 또는 차등 백업에서 RESTORE HEADERONLY 작업을 수행할 수 있습니다.  
  
 *full_backup_directory*  
 전체 백업이 포함 된 디렉터리의 이름을 지정 합니다.  
  
 *differential_backup_directory*  
 차등 백업이 포함 된 디렉터리의 이름을 지정 합니다.  
  
-   경로 및 백업 디렉터리는 이미 존재 해야 하며 정규화 범용 명명 규칙 (UNC) 경로으로 지정 해야 합니다.  
  
-   백업 디렉터리에 경로 로컬 경로 수 없습니다 및 위치 중 하나에 될 수 없습니다는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스 노드.  
  
-   UNC 경로와 백업 디렉터리 이름의 최대 길이 200 자입니다.  
  
-   서버 또는 호스트에서 IP 주소로 지정 되어야 합니다.  
  
 RESTORE HEADERONLY  
 한 명의 사용자 데이터베이스 백업에 대 한 헤더 정보만 반환 하도록 지정 합니다. 다른 필드 간의 헤더는 백업 및 백업 이름에 대 한 텍스트 설명을 포함합니다. 백업 이름 백업 파일을 저장 하는 디렉터리의 이름이 같이 필요는 없습니다.  
  
 RESTORE HEADERONLY 결과 패턴화 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 결과입니다. 결과 모두에서 사용 되는 열이 50 개 이상의 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 에 대 한 설명은 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 결과 참조 하십시오. [RESTORE headeronly&#40; Transact SQL &#41; ](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 필요는 **CREATE ANY DATABASE** 권한.  
  
 액세스 하 고 백업 디렉터리에서 읽을 수 있는 권한을 가진 Windows 계정이 필요 합니다. Windows 계정 이름 및 암호에도 저장 해야 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
1.  확인 하려면 자격 증명이 이미를 사용 하는 [sys.dm_pdw_network_credentials &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  를 추가 하거나 자격 증명을 업데이트 하려면 사용 하 여 [sp_pdw_add_network_credentials &#40; SQL 데이터 웨어하우스 &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  자격 증명을 제거 하려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]를 사용 하 여 [sp_pdw_remove_network_credentials &#40; SQL 데이터 웨어하우스 &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>오류 처리  
 RESTORE DATABASE 명령 다음과 같은 오류가 발생합니다.  
  
-   이미 데이터베이스의 이름이 대상 기기에 있습니다. 이 방지 하려면 고유한 데이터베이스 이름을 선택 하거나 restore를 실행 하기 전에 기존 데이터베이스를 삭제 합니다.  
  
-   백업 디렉터리에 백업 파일의 잘못 된 집합이 있습니다.  
  
-   로그인 권한이 데이터베이스를 복원 하는 데 충분 하지 않습니다.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]백업 파일이 있는 네트워크 위치에 올바른 사용 권한이 없는지 않습니다 합니다.  
  
-   백업 디렉터리에 대 한 네트워크 위치에 존재 하지 않는 또는 사용할 수 없습니다.  
  
-   계산 노드 또는 제어 노드에 충분 한 디스크 공간이 있습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]복원을 시작 하기 전에 어플라이언스에 충분 한 디스크 공간이 있는지를 확인 하지 않습니다. 따라서 RESTORE DATABASE 문을 실행 하는 동안-디스크-공간 부족 오류가 발생 하는 것이 같습니다. 디스크 공간 부족 발생할 때 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 복원을 롤백합니다.  
  
-   데이터베이스를 복원 하는 대상 기기에 있는 데이터베이스를 백업한 원본 어플라이언스 보다 더 적은 계산 노드 있습니다.  
  
-   데이터베이스 백업에서 트랜잭션 내에서 시도 됩니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]데이터베이스 복원의 성공 여부를 추적합니다. 차등 데이터베이스 백업 복원 전에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 성공적으로 전체 데이터베이스 복원 완료를 확인 합니다.  
  
 사용자 데이터베이스는 복원 후 데이터베이스 호환성 수준 120을 갖게 됩니다. 이 원래 호환성 수준에 관계 없이 모든 데이터베이스에도 마찬가지입니다.  
  
 **계산 노드 수가 많으면 어플라이언스에 복원**  
실행 [DBCC SHRINKLOG (Azure SQL 데이터 웨어하우스)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 재배포 하면 트랜잭션 로그 증가 하므로을 크게 더 작은 기기에서 데이터베이스를 복원한 후 합니다.  

할당 된 데이터베이스 크기 계산 노드 수에 비례하여 증가 계산 노드 수가 많으면 어플라이언스에 백업을 복원 합니다.  
  
예를 들어 60 GB 복원 만든 데이터베이스 2 개 노드 기기 (30GB 노드당)에서 6 개 노드 어플라이언스에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 6 개 노드 기기에서 180 GB 데이터베이스 (6 노드 30GB 노드당)를 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]처음 두 노드 소스 구성과 일치 하도록 데이터베이스를 복원 하 고 6 노드 모두에 데이터를 다시 배포 합니다.  
  
 재배포 한 후 각 계산 노드가 더 적은 실제 데이터와 더 많은 여유 공간 보다 작은 원본 어플라이언스의 각 계산 노드가 포함 됩니다. 데이터베이스에 더 많은 데이터를 추가 하는 추가 공간을 사용 합니다. 복원 된 데이터베이스 크기가 필요한 것 보다 더 큰 경우 사용할 수 있습니다 [ALTER database&#40; 병렬 데이터 웨어하우스 &#41; ](../../t-sql/statements/alter-database-parallel-data-warehouse.md) 데이터베이스 파일 크기를 축소 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 이러한 제한 사항 및 제한 사항을 원본 어플라이언스 데이터베이스 백업을 만든와 대상 어플라이언스는 데이터베이스를 복원할 어플라이언스 기기가입니다.  
  
 데이터베이스 복원 통계가 자동으로 빌드하지 않습니다.  
  
 하나의 RESTORE DATABASE 또는 BACKUP DATABASE 문을 언제 든 지 기기에서 실행할 수 있습니다. 어플라이언스에 큐에 저장 되며 하나 처리 백업 및 복원에 대 한 여러 문을 동시에 전송 하는 경우 한 번에 있습니다.  
  
 데이터베이스 백업 에서만 복원할 수 있습니다는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 대상 어플라이언스에 동일한 번호 또는 원본 어플라이언스 보다 더 많은 계산 노드 수입니다. 대상 기기 원본 어플라이언스 보다 더 적은 계산 노드를 가질 수 없습니다.  
  
 SQL Server 2012 PDW 하드웨어를 가진 SQL Server 2008 R2 하드웨어 어플라이언스에 있는 기기에서 생성 된 백업을 복원할 수 없습니다. 어플라이언스에 원래 SQL Server 2008 R2 PDW 하드웨어 함께 구매 하 고 이제 SQL Server 2012 PDW 소프트웨어를 실행 하는 경우에 마찬가지입니다.  
  
## <a name="locking"></a>잠금  
 데이터베이스 개체에 대 한 단독 잠금을 사용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-restore-examples"></a>1. 간단한 복원 예제  
 다음 예제에는 전체 백업을 복원는 `SalesInvoices2013` 데이터베이스입니다. 백업 파일에 저장 됩니다는 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 디렉터리입니다. SalesInvoices2013 데이터베이스는 대상 기기에서 이미 있을 수 없습니다 또는 오류가 발생 하 여이 명령은 실패 합니다.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>2. 전체 및 차등 백업 복원  
 다음 예에서는를 SalesInvoices2013 데이터베이스는 전체 및 차등 백업 복원  
  
 데이터베이스의 전체 백업에 저장 되는 전체 백업에서 복원 되는 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full' 디렉터리입니다. 복원을 성공적으로 완료 되 면 SalesInvoices2013 데이터베이스에 차등 백업이 복원 됩니다.  차등 백업에 저장 되는 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff' 디렉터리입니다.  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>3. 백업 헤더를 복원합니다.  
 데이터베이스 백업에 대 한 헤더 정보를 복원 하는이 예제 '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'. 이 명령은 한 Invoices2013Full 백업에 대 한 정보 행에 발생합니다.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 백업의 내용을 확인 하거나 백업 복원을 시도 하기 전에 대상 복원 기기 원본 백업 어플라이언스와 호환 되는지 확인 하는 헤더 정보를 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 백업 &#40; 병렬 데이터 웨어하우스 &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
