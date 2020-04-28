---
title: Master 데이터베이스
description: 병렬 데이터 웨어하우스의 master 데이터베이스에 대해 알아봅니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafef8a5b702b6df4475d34e9395bb12bc9461fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400983"
---
# <a name="master-database---parallel-data-warehouse"></a>Master 데이터베이스-병렬 데이터 웨어하우스
SQL Server PDW master 데이터베이스는 어플라이언스 수준 로그인 정보 및 데이터베이스 카탈로그를 저장 합니다. 이는 컨트롤 노드에 있는 SQL Server master 데이터베이스입니다. 따라서 master에서 SQL Server에 제공 하는 것과 비슷한 기능을 SQL Server PDW 합니다.  
  
시스템 데이터베이스에 대 한 자세한 내용은 [시스템 데이터베이스](system-databases.md)를 참조 하세요.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
다음 목록에서는 SQL Server PDW master 데이터베이스에서 수행할 수 없는 작업에 대해 설명 합니다.  
  
다음을 할 *수 없습니다.*  
  
-   Master의 차등 백업을 수행 합니다.  
  
-   Master에 사용자 개체를 만듭니다.  
  
-   Master의 데이터 정렬을 변경 합니다.  
  
-   마스터의 소유자를 변경 합니다.  
  
-   Master를 삭제 하거나 이름을 바꿉니다.  
  
-   Master에 대 한 사용 권한을 수정 합니다.  
  
-   **DBCC SHRINKLOG**를 실행 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|작업|설명|  
|--------|---------------|  
|Master의 전체 백업을 만듭니다.|예제:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />자세한 내용은 [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)를 참조 하세요.|  
|master 데이터베이스 복원|Master 데이터베이스를 복원 하려면 Configuration Manager 도구의 [Master 데이터베이스 복원](restore-the-master-database.md) 페이지를 사용 합니다.|  
|데이터베이스 카탈로그 정보를 봅니다.|`SELECT * FROM master.sys.databases;`|  
|시스템 전체 로그인 및 사용 권한 정보를 확인 합니다.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
