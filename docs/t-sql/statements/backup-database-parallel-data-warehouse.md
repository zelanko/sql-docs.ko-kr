---
title: BACKUP DATABASE(병렬 데이터웨어 하우스) | Microsoft 문서 도구
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ad9d69b045a149bf6adad58f16f881ccc5d98e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783484"
---
# <a name="backup-database-parallel-data-warehouse"></a>BACKUP DATABASE(병렬 데이터웨어 하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스의 백업을 만들고 사용자 지정 네트워크 위치에 어플라이언스의 백업을 저장합니다. 재해 복구를 하거나 하나의 어플라이언스에서 다른 어플라이언스로 데이터베이스를 복사하려면 [RESTORE DATABASE&#40;병렬 데이터 웨어하우스&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)와 함께 이 명령문을 사용합니다.  
  
 **시작하기 전에**, [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "백업 서버 확보 및 구성"을 참조하세요.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에는 두 가지 백업 유형이 있습니다. *전체 데이터베이스 백업*은 전체 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스의 백업입니다. *차등 데이터베이스 백업*에는 마지막 전체 백업 이후의 변경 내용만 포함됩니다. 사용자 데이터베이스 백업에는 데이터베이스 사용자 및 데이터베이스 역할이 포함됩니다. master 데이터베이스 백업에는 로그인 정보가 포함됩니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 백업에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에 있는 "백업 및 복원"을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
      Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 백업을 만들 데이터베이스의 이름입니다. 데이터베이스는 master 데이터베이스 또는 사용자 데이터베이스가 될 수 있습니다.  
  
 TO DISK = '\\\\*UNC_path*\\*backup_directory*'  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]이 백업 파일을 작성할 네트워크 경로 및 디렉토리입니다. 예: '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
-   백업 디렉터리 이름에 대한 경로가 이미 존재해야 하며 정규화된 UNC(범용 명명 규칙) 경로로 지정해야합니다.  
  
-   백업 명령을 실행하기 전에는 백업 디렉토리 *backup_directory*가 없어야 합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 백업 디렉토리를 만듭니다.  
  
-   백업 디렉토리 경로는 로컬 경로일 수 없으며 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스 노드의 위치일 수 없습니다.  
  
-   UNC 경로 및 백업 디렉터리 이름의 최대 길이는 200자입니다.  
  
-   서버 또는 호스트는 IP 주소로 지정해야 합니다.  그것을 호스트 또는 서버 이름으로 지정할 수 없습니다.  
  
 DESCRIPTION = **'***text***'**  
 백업에 대한 텍스트 설명을 지정합니다. 최대 텍스트 길이는 255자입니다.  
  
 설명은 메타데이터에 저장되며, 백업 헤더가 RESTORE HEADERONLY를 사용하여 복원될 때 표시됩니다.  
  
 NAME = **'***backup _name***'**  
 백업의 이름을 지정합니다. 백업 이름은 데이터베이스 이름과 다를 수 있습니다.  
  
-   이름은 최대 128자까지 지정할 수 있습니다.  
  
-   경로를 포함할 수 없습니다.  
  
-   문자, 숫자 또는 밑줄(_)로 시작해야 합니다. 허용되는 특수 문자는 밑줄(\_), 하이픈(-) 또는 공백( )입니다. 백업 이름은 공백 문자로 끝날 수 없습니다.  
  
-   *backup_name*이 지정된 위치에 이미 존재하면 문은 실패합니다.  
  
 이 이름은 메타데이터에 저장되며, 백업 헤더가 RESTORE HEADERONLY를 사용하여 복원될 때 표시됩니다.  
  
 DIFFERENTIAL  
 사용자 데이터베이스의 차등 백업을 수행하도록 지정합니다. 생략할 경우 기본값은 전체 데이터베이스 백업입니다. 차등 백업의 이름이 전체 백업의 이름과 일치할 필요는 없습니다. 차등 및 해당하는 전체 백업을 추적하려면 동일한 이름에 'full' 또는 'diff'를 추가하여 사용하는 것이 좋습니다.  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>사용 권한  
 **db_backupoperator** 고정 데이터베이스 역할에서 **BACKUP DATABASE** 권한 또는 멤버 자격이 필요합니다. master 데이터베이스는 백업할 수 없지만 **db_backupoperator** 고정 데이터베이스 역할에 추가된 일반 사용자의 경우 할 수 있습니다. master 데이터베이스는 **sa**, 패브릭 관리자 또는 **sysadmin** 고정 서버 역할을 하는 멤버만이 백업할 수 있습니다.  
  
 백업 디렉토리에 액세스하고, 만들고, 쓸 수 있는 권한이 있는 Windows 계정이 필요합니다. 또한 Windows 계정 이름 및 암호를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 저장해야 합니다. 이러한 네트워크 자격 증명을 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 추가하려면 [sp_pdw_add_network_credentials&#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로 시저를 사용합니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서의 자격 증명 관리에 대한 자세한 내용은 [보안](#Security) 섹션을 참조하세요.  
  
## <a name="error-handling"></a>오류 처리  
 다음 조건에서 BACKUP DATABASE 오류가 발생합니다.  
  
-   사용자 권한은 백업을 수행하기에 충분하지 않습니다.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 백업이 저장될 네트워크 위치에 대한 올바른 사용 권한이 없습니다.  
  
-   데이터베이스가 없습니다.  
  
-   대상 디렉터리가 네트워크 공유에 이미 있습니다.  
  
-   대상 네트워크 공유를 사용할 수 없습니다.  
  
-   대상 네트워크 공유에 백업을 위한 충분한 공간이 없습니다. BACKUP DATABASE 명령은 백업을 시작하기에 앞서 디스크 공간이 충분한지 확인하지 않으므로 BACKUP DATABASE를 실행하는 동안 디스크 공간 부족 오류가 일어날 수 있습니다. 디스크 공간이 부족하면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 BACKUP DATABASE 명령을 롤백합니다. 데이터베이스의 크기를 줄이려면 [DBCC SHRINKLOG(Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)를 실행합니다.  
  
-   트랜잭션 내에서 백업을 시작하려고 시도합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 데이터베이스 백업을 수행하기 전에 [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)를 사용하여 데이터베이스의 크기를 줄입니다. 
 
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업은 동일한 디렉토리에 여러 파일의 집합으로 저장됩니다.  
  
 차등 백업은 일반적으로 전체 백업보다 시간이 적게 들며 더 자주 수행할 수 있습니다. 여러 차등 백업이 동일한 전체 백업을 기반으로 하는 경우 각 차등 백업에는 이전 차등 백업의 모든 변경 사항이 포함됩니다.  
  
 BACKUP 명령을 취소하면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 대상 디렉토리 및 백업을 위해 생성된 모든 파일을 제거합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]의 공유에 대한 네트워크 연결이 끊어지면 롤백을 완료할 수 없습니다.  
  
 전체 백업과 차등 백업은 서로 다른 디렉토리에 저장됩니다. 전체 백업과 차등 백업이 서로 관련 있음을 나타내기 위한 명명 규칙이 강제되지 않습니다. 자신 만의 명명 규칙을 통해 이 관련성을 추적할 수 있습니다. 또는 WITH DESCRIPTION 옵션을 사용하여 설명을 추가한 다음, RESTORE HEADERONLY 문을 사용하여 설명을 검색할 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 master 데이터베이스의 차등 백업을 수행할 수 없습니다. master 데이터베이스의 전체 백업 만 지원됩니다.  
  
 백업 파일은 [RESTORE DATABASE&#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md) 문을 사용하여 백업을 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스에 복원하는데 적합한 형식으로만 저장됩니다.  
  
 BACKUP DATABASE 문을 사용한 백업은 데이터 또는 사용자 정보를 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스로 전송하는 데 사용할 수 없습니다. 그 기능을 위해서는 원격 테이블 복사 기능을 사용할 수 있습니다. 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]에서 "원격 테이블 복사"를 참조하세요.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 기술을 사용하여 데이터베이스를 백업하고 복원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 옵션은 백업 압축을 사용하도록 미리 구성됩니다. 압축, 체크섬, 블록 크기 및 버퍼 개수 등의 백업 옵션을 설정할 수 없습니다.  
  
 주어진 시간에 어플라이언스에서 오직 하나의 데이터베이스 백업 또는 복원만을 실행할 수 있습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 현재 백업 또는 복원 명령이 완료될 때까지 백업 또는 복원 명령을 대기열에 넣습니다.  
  
 백업을 복원하기 위한 대상 어플라이언스에는 적어도 원본 어플라이언스와 같은 정도의 Compute 노드가 있어야 합니다. 대상이 원본 어플라이언스보다 계산 노드를 많이 가질 수는 있으나 적게 가질 수는 없습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 백업이 어플라이언스에 저장되므로 백업의 위치와 이름을 추적하지 않습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 데이터베이스 백업의 성공 또는 실패를 추적합니다.  
  
 차등 백업은 마지막 전체 백업이 성공적으로 완료된 경우에만 허용됩니다. 예를 들어 월요일에 판매 데이터베이스의 전체 백업을 만들었고 백업이 성공적으로 완료되었다고 가정합니다. 그런 다음, 화요일에 판매 데이터베이스의 전체 백업을 다시 만들고 실패합니다. 이 실패 후에는 월요일의 전체 백업을 기반으로 차등 백업을 만들 수 없습니다. 차등 백업을 만들기 전에 먼저 성공적인 전체 백업을 만들어야합니다.  
  
## <a name="metadata"></a>메타데이터  
 이러한 동적 관리 뷰에는 모든 백업, 복원 및 로드 작업에 대한 정보가 들어 있습니다. 이 정보는 시스템을 다시 시작해도 유지됩니다.  
  
-   [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>성능  
 백업을 수행하려면, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 먼저 메타데이터를 백업한 다음, 계산 노드에 저장된 데이터베이스 데이터의 병렬 백업을 수행합니다. 데이터는 각 계산 노드에서 백업 디렉토리로 직접 복사됩니다. 최상의 성능으로 데이터를 계산 노드에서 백업 디렉토리로 옮기기 위해 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 동시에 데이터를 복사하는 계산 노드의 수를 조정합니다.  
  
## <a name="locking"></a>잠금  
 DATABASE 개체에서 ExclusiveUpdate 잠금을 얻습니다.  
  
##  <a name="Security"></a> 보안  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업은 어플라이언스에 저장되지 않습니다. 따라서 IT 팀은 백업 보안의 모든 측면을 관리하는 일을 담당합니다. 예를 들어, 여기에는 백업 데이터의 보안, 백업을 저장하는데 사용되는 서버의 보안 및 백업 서버를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 기기에 연결하는 네트워킹 인프라의 보안 관리가 포함됩니다.  
  
 **네트워크 자격 증명 관리**  
  
 백업 디렉터리에 대한 네트워크 액세스는 표준 Windows 파일 공유 보안을 기반으로 합니다. 백업을 수행하기 전에 백업 디렉토리에 대해 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]을 인증하는 데 사용할 Windows 계정을 만들거나 지정해야 합니다. 이 Windows 계정에는 백업 디렉토리에 액세스, 작성 및 쓰기할 수 있는 권한이 있어야 합니다.  
  
> [!IMPORTANT]  
>  데이터의 보안 위험을 줄이려면 Windows 계정 하나를 전적으로 백업 및 복원 작업을 수행할 목적으로 지정하는 것이 좋습니다. 이 계정에 전적으로 백업 위치에 대해서만 권한을 갖도록 허용합니다.  
  
 [sp_pdw_add_network_credentials&#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로 시저를 실행하여 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 사용자 이름 및 암호를 저장해야 합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 Windows Credential Manager를 사용하여 사용자 이름과 암호를 제어 노드와 계산 노드에 저장하고 암호화합니다. 자격 증명은 BACKUP DATABASE 명령으로 백업되지 않습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 네트워크 자격 증명을 제거하려면 [sp_pdw_remove_network_credentials&#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)를 참조하세요.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에 저장된 모든 네트워크 자격 증명을 나열하려면 [sys.dm_pdw_network_credentials&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 동적 관리 뷰를 사용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>1. 백업 위치에 대한 네트워크 자격 증명 추가  
 백업을 만들려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에게 백업 디렉토리에 대한 읽기/쓰기 권한이 있어야 합니다. 다음 예제에서는 사용자에 대한 자격 증명을 추가하는 방법을 보여 줍니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 이러한 자격 증명을 저장하고 백업 및 복원 작업에 그것을 사용합니다.  
  
> [!IMPORTANT]  
>  보안상의 이유로 하나의 도메인 계정을 전적으로 백업을 수행할 목적으로 만드는 것이 좋습니다.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>2. 백업 위치에 대한 네트워크 자격 증명 제거  
 다음 예에서는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 도메인 사용자의 자격 증명을 제거하는 방법을 보여줍니다.  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>3. 사용자 데이터베이스의 전체 백업 만들기  
 다음 예에서는 송장 사용자 데이터베이스의 전체 백업을 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 Invoices2013 디렉토리를 만들고 백업 파일을 \\\10.192.63.147\backups\yearly\Invoices2013Full 디렉토리에 저장합니다.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>4. 사용자 데이터베이스의 전체 백업 만들기  
 다음 예에서는 송장 데이터베이스의 마지막 전체 백업 이후에 발생한 모든 변경 내용을 포함하는 차등 백업을 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]은 파일을 저장할 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 디렉토리를 만듭니다. '송장 2013 차등 백업' 설명이 백업에 대한 헤더 정보와 함께 저장됩니다.  
  
 차등 백업은 송장의 마지막 전체 백업이 성공적으로 완료된 경우에만 성공적으로 실행됩니다.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>5. master 데이터베이스의 전체 백업 만들기  
 다음 예제에서는 master 데이터베이스의 전체 백업을 만들고 '\\\10.192.63.147\backups\2013\daily\20130722\master' 디렉터리에 저장합니다.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>6. 어플라이언스 로그인 정보의 백업을 만듭니다.  
 마스터 데이터베이스는 어플라이언스 로그인 정보를 저장합니다. 어플라이언스 로그인 정보를 백업하려면 master를 백업해야 합니다.  
  
 다음 예에서는 마스터 데이터베이스의 백업을 만듭니다.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>참고 항목  
 [RESTORE DATABASE&#40;병렬 데이터 웨어하우스&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
