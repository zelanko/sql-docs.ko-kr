---
title: "데이터베이스 스냅숏 스파스 파일의 크기 보기(Transact-SQL) | Microsoft 문서"
ms.date: 07/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
caps.latest.revision: "41"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1696e51f0f523a98f3bc3acdbb36bd97b9cf0f22
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>데이터베이스 스냅숏 스파스 파일의 크기 보기(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일이 스파스 파일인지 확인하고 이 파일의 실제 크기 및 최대 크기를 찾는 방법을 보여 줍니다. NTFS 파일 시스템의 기능인 스파스 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 스냅숏에 사용됩니다.  
  
> [!NOTE]  
>  데이터베이스 스냅숏을 만드는 동안 CREATE DATABASE 문의 파일 이름을 사용하여 스파스 파일을 만듭니다. 이러한 파일 이름은 **physical_name** 열의 **sys.master_files** 에 저장됩니다. **sys.database_files** (원본 데이터베이스 또는 스냅숏에 있음)의 **physical_name** 열에는 항상 원본 데이터베이스 파일 이름이 있습니다.  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>데이터베이스 파일이 스파스 파일인지 확인  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 다음을 수행합니다.  
  
     데이터베이스 스냅숏의 **sys.database_files** 또는 **sys.master_files** 에서 **is_sparse**열을 선택합니다. 이 값은 다음과 같이 파일이 스파스 파일인지 여부를 나타냅니다.  
  
     1 = 스파스 파일입니다.  
  
     0 = 스파스 파일이 아닙니다.  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>스파스 파일의 실제 크기 확인  
  
> [!NOTE]  
>  스파스 파일은 64KB씩 증분되므로 디스크상의 스파스 파일 크기는 항상 64KB의 배수입니다.  
  
 스냅숏의 각 스파스 파일이 현재 디스크에서 사용 중인 바이트 수를 확인하려면 **sys.dm_io_virtual_file_stats** 동적 관리 뷰의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][size_on_disk_bytes](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) 열을 쿼리합니다.  
  
 스파스 파일이 사용하는 디스크 공간을 보려면 Microsoft Windows에서 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하여 **디스크 할당 크기** 값을 봅니다.  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>스파스 파일의 최대 크기 확인  
 스파스 파일이 증가할 수 있는 최대 크기는 스냅숏을 작성한 시점의 해당 원본 데이터베이스 파일 크기입니다. 이 크기를 확인하는 데 사용할 수 있는 방법은 다음과 같습니다.  
  
-   Windows 명령 프롬프트 사용:  
  
    1.  Windows **dir** 명령을 사용합니다.  
  
    2.  Windows에서 스파스 파일을 선택하고 **속성** 대화 상자를 연 다음 **크기** 값을 봅니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 다음을 수행합니다.  
  
     데이터베이스 스냅숏의 **sys.database_files** 또는 **sys.master_files** 에서 **size**열을 선택합니다. **size** 열의 값은 SQL 페이지에서 스냅숏이 사용할 수 있는 최대 공간을 반영합니다. 이 값은 파일의 SQL 페이지 수를 기준으로 표시된다는 점을 제외하고 Windows **크기** 필드에 해당하며 바이트 단위의 크기는 다음과 같습니다.  
  
     ( *number_of_pages* * 8192)  

## <a name="example"></a>예제
다음 스크립트는 각 스파스 파일에 대한 디스크 크기(킬로바이트)를 보여 줍니다.  스크립트는 또한 스파스 파일이 늘어날 수 있는 최대 크기(메가바이트)도 보여 줍니다.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 TRANSACT-SQL 스크립트를 실행합니다.

```sql
SELECT  DB_NAME(sd.source_database_id) AS [SourceDatabase], 
        sd.name AS [Snapshot],
        mf.name AS [Filename], 
        size_on_disk_bytes/1024 AS [size_on_disk (KB)],
        mf2.size/128 AS [MaximumSize (MB)]
FROM sys.master_files mf
JOIN sys.databases sd
    ON mf.database_id = sd.database_id
JOIN sys.master_files mf2
    ON sd.source_database_id = mf2.database_id
    AND mf.file_id = mf2.file_id
CROSS APPLY sys.dm_io_virtual_file_stats(sd.database_id, mf.file_id)
WHERE mf.is_sparse = 1
AND mf2.is_sparse = 0
ORDER BY 1;
```
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
