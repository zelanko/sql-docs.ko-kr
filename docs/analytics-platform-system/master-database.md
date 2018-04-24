---
title: Master 데이터베이스-병렬 데이터 웨어하우스 | Microsoft Docs
description: 병렬 데이터 웨어하우스에서 master 데이터베이스에 알아봅니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="master-database---parallel-data-warehouse"></a>Master 데이터베이스-병렬 데이터 웨어하우스
SQL Server PDW 마스터 데이터베이스 수준의 어플라이언스에 로그인 정보 및 데이터베이스 카탈로그에 저장합니다. 제어 노드에 있는 SQL Server 마스터 데이터베이스. 따라서 SQL Server에 제공 하는 마스터 SQL Server PDW에 유사한 기능을 제공 합니다.  
  
시스템 데이터베이스에 대 한 자세한 내용은 참조 [시스템 데이터베이스](system-databases.md)합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
다음 목록에는 SQL Server PDW 마스터 데이터베이스에서 수행할 수 없는 작업을 설명 합니다.  
  
하면 *수 없습니다.*  
  
-   Master의 차등 백업을 수행 합니다.  
  
-   Master에 사용자 개체를 만듭니다.  
  
-   Master의 데이터 정렬을 변경 합니다.  
  
-   마스터의 소유자를 변경 합니다.  
  
-   삭제 또는 마스터 이름을 변경 합니다.  
  
-   마스터에 대 한 수정 합니다.  
  
-   실행 **DBCC SHRINKLOG**합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크|Description|  
|--------|---------------|  
|마스터의 전체 백업을 만듭니다.|예:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />자세한 내용은 참조 [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)합니다.|  
|Master 데이터베이스 복원|사용 하 여 master 데이터베이스 복원의 [Master 데이터베이스 복원](restore-the-master-database.md) 구성 관리자 도구에서 페이지입니다.|  
|데이터베이스 카탈로그 정보를 봅니다.|`SELECT * FROM master.sys.databases;`|  
|시스템 수준 로그인 및 사용 권한 정보를 봅니다.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
