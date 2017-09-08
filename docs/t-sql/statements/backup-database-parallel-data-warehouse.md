---
title: "데이터베이스 백업 (병렬 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4fb36fd89c02ff9ddd5bc33825a387b53ab6e174
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="backup-database-parallel-data-warehouse"></a>데이터베이스 백업 (병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  백업을 만듭니다는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 하 고 어플라이언스에 오프 백업을 네트워크 사용자가 지정한 위치에 저장 합니다. 이 문을 사용 하 여 [데이터베이스 복원 &#40; 병렬 데이터 웨어하우스 &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) 재해 복구를 위한 또는 한 기기에서 데이터베이스를 다른 위치로 복사 합니다.  
  
 **시작 하기 전에**, 획득 및 구성 백업 "서버"에서 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 백업에 두 가지 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. A *전체 데이터베이스 백업을* 전체 백업이 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스입니다. A *차등 데이터베이스 백업을* 마지막 전체 백업 이후 변경 된 내용을 포함 합니다. 데이터베이스 사용자 및 데이터베이스 역할에 사용자 데이터베이스의 백업에 포함 되어 있습니다. Master 데이터베이스의 백업을 로그인이 포함 됩니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 백업, "백업 및 복원"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 백업을 만들 데이터베이스의 이름입니다. 데이터베이스는 master 데이터베이스 또는 사용자 데이터베이스 수 있습니다.  
  
 디스크 = '\\\\*UNC_path*\\*backup_directory*'  
 네트워크 경로 디렉토리를 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 에서는 백업 파일에 기록 합니다. 예를 들어 '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
-   백업 디렉터리 이름에 대 한 경로 이미 존재 해야 하며 정규화 범용 명명 규칙 (UNC) 경로으로 지정 해야 합니다.  
  
-   백업 디렉터리 *backup_directory*, 백업 명령을 실행 하기 전에 없어야 합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]백업 디렉터리를 만듭니다.  
  
-   백업 디렉터리에 경로 로컬 경로 수 없습니다 및 위치 중 하나에 될 수 없습니다는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스 노드.  
  
-   UNC 경로와 백업 디렉터리 이름의 최대 길이 200 자입니다.  
  
-   서버 또는 호스트에서 IP 주소로 지정 되어야 합니다.  호스트 또는 서버 이름으로이 지정할 수 없습니다.  
  
 설명 = **'***텍스트***'**  
 백업에 대 한 텍스트 설명을 지정합니다. 텍스트의 최대 길이 255 자입니다.  
  
 설명에 메타 데이터를 저장 및 백업 헤더 RESTORE HEADERONLY로 복원 하는 경우에 표시 됩니다.  
  
 이름 = **'***백업 _name***'**  
 백업 하는 이름을 지정합니다. 백업 이름을 데이터베이스 이름과 다를 수 있습니다.  
  
-   이름은 최대 128자까지 지정할 수 있습니다.  
  
-   경로 포함할 수 없습니다.  
  
-   문자 또는 숫자 문자 또는 밑줄 (_)로 시작 해야 합니다. 허용 되는 특수 문자는 밑줄 (\_), 하이픈 (-) 또는 공백 (). 백업 이름은 공백 문자로 끝날 수 없습니다.  
  
-   문이 실패 합니다 *백업 _* 지정된 된 위치에 이미 있습니다.  
  
 이 이름은 메타 데이터에 저장 되 고 백업 헤더 RESTORE HEADERONLY로 복원 하는 경우에 표시 됩니다.  
  
 DIFFERENTIAL  
 사용자 데이터베이스의 차등 백업을 수행 하도록 지정 합니다. 생략할 경우 기본값은 전체 데이터베이스 백업 합니다. 차등 백업의 이름 전체 백업의 이름과 일치할 필요는 없습니다. 추적 하 고 해당 하는 전체 백업을 차등, '전체' 또는 'diff' 추가와 동일한 이름을 사용 하는 것이 좋습니다.  
  
 예를 들어  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissions  
 필요는 **BACKUP DATABASE** 권한이 나 멤버 자격에는 **db_backupoperator** 고정된 데이터베이스 역할입니다. 있지만에 추가 된 일반 사용자를 master 데이터베이스를 백업할 수 없습니다는 **db_backupoperator** 고정된 데이터베이스 역할입니다. Master 데이터베이스 에서만를 백업할 수 있습니다 하 여 **sa**는 패브릭 관리자나의 멤버는 **sysadmin** 고정된 서버 역할입니다.  
  
 액세스, 작성 및 백업 디렉터리에 쓸 수 있는 권한을 가진 Windows 계정이 필요 합니다. Windows 계정 이름 및 암호에도 저장 해야 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다. 이러한 네트워크 자격 증명을 추가 하려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]를 사용 하 여는 [sp_pdw_add_network_credentials &#40; SQL 데이터 웨어하우스 &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로시저입니다.  
  
 에 대 한 자격 증명을 관리 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 참조는 [보안](#Security) 섹션.  
  
## <a name="error-handling"></a>오류 처리  
 다음과 같은 백업 데이터베이스 오류:  
  
-   사용자 권한이 백업을 수행 하는 데 충분 하지 않습니다.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]없는 올바른 권한을 백업이 저장 네트워크 위치에 있습니다.  
  
-   데이터베이스가 존재 하지 않습니다.  
  
-   대상 디렉터리가 네트워크 공유에 이미 있습니다.  
  
-   대상 네트워크 공유를 사용할 수 없는 경우  
  
-   대상 네트워크 공유 백업을 저장할 공간이 부족 합니다. 백업 데이터베이스 명령 백업 데이터베이스를 실행 하는 동안-디스크-공간 부족 오류를 생성 하 여 백업을 시작 하기 전에 충분 한 디스크 공간이 있는지 확인 하지 않으므로 합니다. 디스크 공간 부족 발생할 때 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] BACKUP DATABASE 명령을 롤백하고 있습니다. 데이터베이스의 크기를 줄이려면 실행 [DBCC SHRINKLOG (Azure SQL 데이터 웨어하우스)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   트랜잭션 내에서 백업 시작 하려고 시도 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 사용 하 여 데이터베이스 백업을 수행 하기 전에 [DBCC SHRINKLOG (Azure SQL 데이터 웨어하우스)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 데이터베이스의 크기를 줄이려면 합니다. 
 
 A [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업은 동일한 디렉터리 내에서 여러 파일의 집합으로 저장 됩니다.  
  
 일반적으로 차등 백업은 전체 백업 보다 시간 하며 더 자주 수행 될 수 있습니다. 각 차등을 여러 차등 백업 전체를 같은 백업을 기반으로 이전 차등 백업에 모든 변경 내용을 포함 합니다.  
  
 BACKUP 명령을 취소 하면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 대상 디렉터리와 백업을 위해 생성 된 파일을 제거 합니다. 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 의 네트워크 연결이 끊어지는 공유, 롤백을 완료할 수 없습니다.  
  
 전체 백업과 차등 백업이 별도 디렉터리에 저장 됩니다. 전체 백업 및 차등 백업과 함께 속해 있는지를 지정 하기 위한 명명 규칙 적용 되지 않습니다. 사용자 지정 명명 규칙을 통해이 추적할 수 있습니다. 또는, 설명을 추가 하려면 설명 된 옵션을 사용 하 여 한 다음 설명을 검색 RESTORE HEADERONLY 문 사용 하 여이 추적할 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 Master 데이터베이스의 차등 백업을 수행할 수 없습니다. Master 데이터베이스의 전체 백업만 지원 됩니다.  
  
 백업 파일이 복원에 대 한 백업에 대해서만 적합 한 형식으로 저장 되는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 사용 하 여 어플라이언스에 [데이터베이스 복원 &#40; 병렬 데이터 웨어하우스 &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) 문.  
  
 BACKUP DATABASE 문 사용 하 여 백업을 사용 하 여 SMP를 데이터 또는 사용자 정보를 전송할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스. 해당 기능에 대 한 원격 테이블 복사 기능을 사용할 수 있습니다. 자세한 내용은 "원격 테이블 복사"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 데이터베이스 백업 및 복원에 백업 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]백업 옵션은 백업 압축을 사용 하도록 미리 구성 합니다. 압축, 체크섬, 블록 크기 버퍼 개수 등의 백업 옵션을 설정할 수 없습니다.  
  
 하나의 데이터베이스 백업 또는 복원 언제 든 지 기기에서 실행할 수 있습니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]백업 또는 복원 명령을 현재 백업 될 때까지 대기 됩니다 또는 복원 명령이 완료 되었습니다.  
  
 백업 복원을 위한 대상 기기 원본 어플라이언스과 많은 계산 노드를 가져야 합니다. 대상 소스 기기 보다 더 많은 계산 노드를 가질 수 있지만 더 적은 계산 노드를 가질 수 없습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]위치를 추적 하지 않으며 이후 백업이 저장 되는 백업의 이름을 기기를 해제 합니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]성공 또는 실패의 데이터베이스 백업 추적지 않습니다.  
  
 차등 백업은 마지막 전체 백업이 성공적으로 완료 하는 경우에 허용 됩니다. 예를 들어 월요일에 Sales 데이터베이스의 전체 백업을 만들면 및 백업을 성공적으로 완료 합니다. 그런 다음 화요일에 Sales 데이터베이스의 전체 백업을 만들고 실패 합니다. 이 오류가 발생 한 후 다음 월요일의 전체 백업을 기반으로 차등 백업은 만들 수 없습니다. 먼저 차등 백업을 만들기 전에 전체 백업을 만들어야 합니다.  
  
## <a name="metadata"></a>메타데이터  
 이러한 동적 관리 뷰 모두 백업, 복원 하는 방법에 대 한 정보를 포함 하 고 작업을 로드 합니다. 정보는 시스템을 다시 시작 유지합니다.  
  
-   [sys.pdw_loader_backup_runs &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>성능  
 백업을 수행 하려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 첫 번째 백업 메타 데이터를 한 다음 계산 노드에 저장 된 데이터베이스 데이터의 병렬 백업을 수행 합니다. 데이터는 각 계산 노드에서 직접 백업 디렉터리에 복사 됩니다. 백업 디렉터리에는 계산 노드 모두에서 데이터를 이동 하기 위한 최상의 성능을 얻으려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 복사 하는 데이터 동시에 계산 노드 수를 제어 합니다.  
  
## <a name="locking"></a>잠금  
 데이터베이스 개체에 대 한 ExclusiveUpdate 잠금을 얻습니다.  
  
##  <a name="Security"></a> 보안  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]어플라이언스에서 백업 저장 되지 않습니다. 따라서 IT 팀은 백업 보안의 모든 측면을 관리 하는 일을 담당 합니다. 예를 들어 여기에 백업 데이터의 보안, 백업을 저장 하는 데 사용 하는 서버의 보안을 및 백업 서버를 연결 하는 네트워킹 인프라의 보안 관리는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 기기입니다.  
  
 **네트워크 자격 증명 관리**  
  
 백업 디렉터리에 대 한 네트워크 액세스 보안을 공유 하는 표준 Windows 파일을 기반으로 합니다. 만들거나 인증에 사용할 수 있는 Windows 계정을 지정 해야 할 백업을 수행 하기 전에 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업 디렉터리에 있습니다. 이 windows 계정에 액세스, 작성 및 백업 디렉터리에 쓸 수 있는 권한이 있어야 합니다.  
  
> [!IMPORTANT]  
>  데이터와 함께 보안 위험을 줄이기 위해 백업을 실행 하는 목적 으로만 Windows 계정 하나를 지정 하 고 복원 작업 하는 것이 좋습니다. 백업 위치와 다른 위치에 권한을 보유 하도록이 계정을 사용할 수 있음  
  
 사용자 이름 및 암호를 저장 해야 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 를 실행 하 여는 [sp_pdw_add_network_credentials &#40; SQL 데이터 웨어하우스 &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 저장 프로시저입니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Windows 자격 증명 관리자를 사용 하 여 저장 하 고 제어 노드와 계산 노드에 사용자 이름 및 암호를 암호화 합니다. 자격 증명 BACKUP DATABASE 명령을 사용 하 여 백업 하지 않습니다.  
  
 네트워크 자격 증명을 제거 하려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 참조 [sp_pdw_remove_network_credentials &#40; SQL 데이터 웨어하우스 &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 에 저장 된 네트워크 자격 증명을 모두 나열할 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]를 사용 하 여는 [sys.dm_pdw_network_credentials &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 동적 관리 뷰.  
  
## <a name="examples"></a>예  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>1. 백업 위치에 대 한 네트워크 자격 증명을 추가 합니다.  
 백업을 만들려면 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 백업 디렉터리에 읽기/쓰기 권한이 있어야 합니다. 다음 예제에서는 사용자에 대 한 자격 증명을 추가 하는 방법을 보여 줍니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]이러한 자격 증명을 저장 및 사용 하 여 되도록 백업에 대 한 복원 작업입니다.  
  
> [!IMPORTANT]  
>  보안상의 이유로 백업을 수행 하는 목적 으로만 한 도메인 계정을 만드는 것이 좋습니다.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>2. 백업 위치에 대 한 네트워크 자격 증명 제거  
 다음 예제에서 도메인 사용자의 자격 증명을 제거 하는 방법을 보여 줍니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>3. 사용자 데이터베이스의 전체 백업 만들기  
 다음 예제에서는 송장 사용자 데이터베이스의 전체 백업을 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]백업 파일을 저장 및 Invoices2013 디렉터리가 만들어집니다는 \\\10.192.63.147\backups\yearly\Invoices2013Full 디렉터리입니다.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>4. 사용자 데이터베이스의 차등 백업 만들기  
 다음 예제에서는 송장 데이터베이스의 마지막 전체 백업 이후에 발생 한 모든 변경 내용을 포함 하는 차등 백업을 만듭니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]만들어집니다는 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 디렉터리의 파일을 저장 합니다. 설명 '송장 2013 차등 백업에 백업에 대 한 헤더 정보 저장 됩니다.  
  
 송장의 마지막 전체 백업을 성공적으로 완료 하는 경우 차등 백업이 성공적으로 실행 됩니다.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>5. Master 데이터베이스의 전체 백업 만들기  
 다음 예제에서는 master 데이터베이스의 전체 백업을 만들고 디렉터리에 저장 '\\\10.192.63.147\backups\2013\daily\20130722\master'.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>6. 어플라이언스에 로그인 정보의 백업을 만듭니다.  
 Master 데이터베이스 어플라이언스에 로그인 정보를 저장합니다. 어플라이언스에 로그인 정보를 백업 하려면 백업 마스터 합니다.  
  
 다음 예제에서는 master 데이터베이스의 전체 백업을 만듭니다.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 복원 &#40; 병렬 데이터 웨어하우스 &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
