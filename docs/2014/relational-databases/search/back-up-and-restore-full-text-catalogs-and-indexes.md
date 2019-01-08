---
title: 전체 텍스트 카탈로그와 인덱스 백업 및 복원 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], backing up
- full-text search [SQL Server], back up and restore
- recovery [full-text search]
- backups [SQL Server], full-text indexes
- full-text indexes [SQL Server], restoring
- restore operations [full-text search]
ms.assetid: 6a4080d9-e43f-4b7b-a1da-bebf654c1194
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 932263934fe7ce93a50caec468d7f1444ccae181
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372495"
---
# <a name="back-up-and-restore-full-text-catalogs-and-indexes"></a>전체 텍스트 카탈로그와 인덱스 백업 및 복원
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 만든 전체 텍스트 인덱스를 백업 및 복원하는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전체 텍스트 카탈로그는 논리적인 개념이며 파일 그룹에 상주하는 것은 아닙니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전체 텍스트 카탈로그를 백업하려면 카탈로그에 속한 전체 텍스트 인덱스가 포함된 모든 파일 그룹을 식별해야 합니다. 그런 다음 해당 파일 그룹을 하나씩 백업해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 업그레이드할 때 전체 텍스트 카탈로그를 가져올 수도 있습니다. 가져온 각 전체 텍스트 카탈로그는 고유한 파일 그룹에 있는 데이터베이스 파일입니다. 가져온 카탈로그를 백업하려면 해당 파일 그룹을 백업하기만 하면 됩니다. 자세한 내용은 [온라인 설명서의](https://go.microsoft.com/fwlink/?LinkID=121052)전체 텍스트 카탈로그 백업 및 복원 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 을 참조하세요.  
  
##  <a name="backingup"></a> 전체 텍스트 카탈로그의 전체 텍스트 인덱스 백업  
  
###  <a name="Find_FTIs_of_a_Catalog"></a> 전체 텍스트 카탈로그에서 전체 텍스트 인덱스 찾기  
 [sys.fulltext_indexes](/sql/t-sql/queries/select-transact-sql) 및 [sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql) 카탈로그 뷰에서 열을 선택하는 다음과 같은 [SELECT](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql) 문을 사용하여 전체 텍스트 인덱스의 속성을 검색할 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @TableID int;  
SET @TableID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product'));  
SELECT object_name(@TableID), i.is_enabled, i.change_tracking_state,   
   i.has_crawl_completed, i.crawl_type, c.name as fulltext_catalog_name   
   FROM sys.fulltext_indexes i, sys.fulltext_catalogs c   
   WHERE i.fulltext_catalog_id = c.fulltext_catalog_id;  
GO  
```  
  

  
###  <a name="Find_FG_of_FTI"></a> 전체 텍스트 인덱스를 포함하는 파일 그룹 또는 파일 찾기  
 전체 텍스트 인덱스가 생성되면 다음 위치 중 하나로 배치됩니다.  
  
-   사용자가 지정한 파일 그룹  
  
-   분할되지 않은 테이블의 경우 기본 테이블 또는 뷰와 동일한 파일 그룹  
  
-   분할된 테이블의 경우 기본 파일 그룹  
  
> [!NOTE]  
>  전체 텍스트 인덱스 만들기에 대한 정보는 [전체 텍스트 인덱스 만들기 및 관리](create-and-manage-full-text-indexes.md) 및 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)를 참조하세요.  
  
 테이블 또는 뷰에서 전체 텍스트 인덱스의 파일 그룹을 찾으려면 다음 쿼리를 사용합니다. 여기서 *object_name* 은 테이블 또는 뷰의 이름입니다.  
  
```  
SELECT name FROM sys.filegroups f, sys.fulltext_indexes i   
   WHERE f.data_space_id = i.data_space_id   
      and i.object_id = object_id('object_name');  
GO  
  
```  
  

  
###  <a name="Back_up_FTIs_of_FTC"></a> 전체 텍스트 인덱스가 포함된 파일 그룹 백업  
 전체 텍스트 카탈로그의 인덱스를 포함하는 파일 그룹을 찾은 후에는 각 파일 그룹을 백업해야 합니다. 백업 프로세스 중에는 전체 텍스트 카탈로그를 삭제하거나 추가할 수 없습니다.  
  
 파일 그룹의 첫 번째 백업은 전체 파일 백업이어야 합니다. 파일 그룹의 전체 파일 백업을 만들면 전체 파일 백업에 기반을 둔 일련의 차등 파일 백업을 하나 이상 만들어 파일 그룹의 변경 내용만 백업할 수 있습니다.  
  
 **파일과 파일 그룹을 백업하려면**  
  
-   [파일 및 파일 그룹 백업&#40;SQL Server&#41;](../backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  

  
##  <a name="Restore_FTI"></a> 전체 텍스트 인덱스 복원  
 백업된 파일 그룹을 복원하면 전체 텍스트 인덱스 파일과 파일 그룹에 있는 다른 파일들까지 모두 복원됩니다. 기본적으로 파일 그룹은 파일 그룹이 백업된 디스크 위치에 복원됩니다.  
  
 전체 텍스트 인덱싱된 테이블이 온라인 상태이고 백업을 만들 때 채우기가 실행 중이었으면 복원 후 채우기가 다시 시작됩니다.  
  
 **파일 그룹을 복원하려면**  
  
-   [파일 및 파일 그룹 복원&#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [기존 파일에서 파일 및 파일 그룹 복원&#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [새 위치로 파일 복원&#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  

  
## <a name="see-also"></a>관련 항목  
 [서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링](manage-and-monitor-full-text-search-for-a-server-instance.md)   
 [전체 텍스트 검색 업그레이드](upgrade-full-text-search.md)  
  
  
