---
title: "master 데이터베이스 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c71617c0-6689-4f52-81c6-58f4cf7c7377
caps.latest.revision: "8"
ms.workload: not set
ms.openlocfilehash: 59acb3fb8c5c1913e8b4d656e9895b2810e19497
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="master-database"></a>master 데이터베이스
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
  
## <a name="related-tasks"></a>관련 태스크  
  
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
  
