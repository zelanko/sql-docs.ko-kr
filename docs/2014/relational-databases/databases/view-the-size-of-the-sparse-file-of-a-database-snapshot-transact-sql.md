---
title: 데이터베이스 스냅샷 스파스 파일의 크기 보기(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
author: stevestein
ms.author: sstein
ms.openlocfilehash: 424399b9915c8e7e26e1076fd2e553aafe06fcf0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969934"
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>데이터베이스 스냅샷 스파스 파일의 크기 보기(Transact-SQL)
  이 항목에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일이 스파스 파일인지 확인하고 이 파일의 실제 크기 및 최대 크기를 찾는 방법을 보여 줍니다. NTFS 파일 시스템의 기능인 스파스 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 스냅샷에 사용됩니다.  
  
> [!NOTE]  
>  데이터베이스 스냅샷을 만드는 동안 CREATE DATABASE 문의 파일 이름을 사용하여 스파스 파일을 만듭니다. 이러한 파일 이름은 **physical_name** 열의 **sys.master_files** 에 저장됩니다. **sys.database_files** (원본 데이터베이스 또는 스냅샷에 있음)의 **physical_name** 열에는 항상 원본 데이터베이스 파일 이름이 있습니다.  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>데이터베이스 파일이 스파스 파일인지 확인  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 다음을 수행합니다.  
  
     데이터베이스 스냅샷의 **sys.database_files** 또는 **sys.master_files** 에서 **is_sparse**열을 선택합니다. 이 값은 다음과 같이 파일이 스파스 파일인지 여부를 나타냅니다.  
  
     1 = 스파스 파일입니다.  
  
     0 = 스파스 파일이 아닙니다.  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>스파스 파일의 실제 크기 확인  
  
> [!NOTE]  
>  스파스 파일은 64KB씩 증분되므로 디스크상의 스파스 파일 크기는 항상 64KB의 배수입니다.  
  
 스냅샷의 각 스파스 파일이 현재 디스크에서 사용 중인 바이트 수를 확인하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][sys.dm_io_virtual_file_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql) 동적 관리 뷰의 **size_on_disk_bytes** 열을 쿼리합니다.  
  
 스파스 파일이 사용하는 디스크 공간을 보려면 Microsoft Windows에서 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하여 **디스크 할당 크기** 값을 봅니다.  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>스파스 파일의 최대 크기 확인  
 스파스 파일이 증가할 수 있는 최대 크기는 스냅샷을 작성한 시점의 해당 원본 데이터베이스 파일 크기입니다. 이 크기를 확인하는 데 사용할 수 있는 방법은 다음과 같습니다.  
  
-   Windows 명령 프롬프트 사용:  
  
    1.  Windows **dir** 명령을 사용합니다.  
  
    2.  Windows에서 스파스 파일을 선택하고 **속성** 대화 상자를 연 다음 **크기** 값을 봅니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 다음을 수행합니다.  
  
     데이터베이스 스냅샷의 **sys.database_files** 또는 **sys.master_files** 에서 **size**열을 선택합니다. **size** 열의 값은 SQL 페이지에서 스냅샷이 사용할 수 있는 최대 공간을 반영합니다. 이 값은 파일의 SQL 페이지 수를 기준으로 표시된다는 점을 제외하고 Windows **크기** 필드에 해당하며 바이트 단위의 크기는 다음과 같습니다.  
  
     ( *number_of_pages* * 8192)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 스냅숏은 SQL Server를 &#40;&#41;](database-snapshots-sql-server.md)   
 [fn_virtualfilestats &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql)   
 [database_files &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
  
