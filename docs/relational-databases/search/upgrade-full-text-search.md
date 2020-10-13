---
description: 전체 텍스트 검색 업그레이드
title: 전체 텍스트 검색 업그레이드 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], installing
- migrating full-text indexes [SQL Server]
- upgrading Full-Text Search
- installing Full-Text Search
- full-text search [SQL Server], upgrading
ms.assetid: 2fee4691-f2b5-472f-8ccc-fa625b654520
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4759838a20e721031db8e4ea5e644cc3822285a8
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868940"
---
# <a name="upgrade-full-text-search"></a>전체 텍스트 검색 업그레이드
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  설치 프로그램을 실행하거나 데이터베이스 복사 마법사를 사용하여 이전 버전의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 만든 데이터베이스 파일 및 전체 텍스트 카탈로그를 연결, 복원 또는 복사하면 전체 텍스트 검색이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 업그레이드됩니다.  
  
  
##  <a name="upgrade-a-server-instance"></a><a name="Upgrade_Server"></a> 서버 인스턴스 업그레이드  
 전체 업그레이드를 수행할 수 있도록 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 인스턴스가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 설치되고 데이터가 마이그레이션됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 전체 텍스트 검색이 설치된 경우 새 버전의 전체 텍스트 검색이 자동으로 설치됩니다. 함께 설치되었다는 것은 다음과 같은 구성 요소가 각각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스 수준에 있음을 의미합니다.  
  
 단어 분리기, 형태소 분석기 및 필터  
 각 인스턴스는 단어 분리기, 형태소 분석기 및 필터의 자체 집합을 사용하며 이러한 구성 요소의 운영 체제 버전에 더 이상 의존하지 않습니다. 또한 이러한 구성 요소를 인스턴스 단위 수준에서 보다 쉽게 등록하고 구성할 수 있습니다. 자세한 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) 및 [검색 필터 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)를 참조하세요.  
  
 필터 데몬 호스트  
 전체 텍스트 필터 데몬 호스트는 전체 텍스트 엔진의 무결성을 유지하면서 인덱스 및 쿼리에 사용되는 단어 분리기, 형태소 분석기 및 필터 등의 확장 가능한 외부 구성 요소를 안전하게 로드하고 실행하는 프로세스입니다. 서버 인스턴스는 모든 다중 스레드 필터에 대해 다중 스레드 프로세스를 사용하고 모든 단일 스레드 필터에 대해 단일 스레드 프로세스를 사용합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 에는 FDHOST Launcher 서비스(MSSQLFDLauncher)를 위한 서비스 계정이 도입되었습니다. 이 서비스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 인스턴스의 필터 데몬 호스트 프로세스에 서비스 계정 정보를 전파합니다. 서비스 계정을 설정하는 방법은 [전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)을 참조하세요.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 각 전체 텍스트 인덱스가 파일 그룹에 속하는 전체 텍스트 카탈로그에 있고 실제 경로를 가지며 데이터베이스 파일로 처리됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그는 전체 텍스트 인덱스의 그룹을 포함하는 논리적 개체 또는 가상 개체입니다. 따라서 새로운 전체 텍스트 카탈로그는 실제 경로가 있는 데이터베이스 파일로 취급되지 않습니다. 그러나 데이터 파일이 들어 있는 전체 텍스트 카탈로그를 업그레이드할 때는 같은 디스크에 새 파일 그룹이 만들어집니다. 따라서 업그레이드 후에도 이전의 디스크 I/O 동작이 유지됩니다. 루트 경로가 있으면 해당 카탈로그의 전체 텍스트 인덱스가 새 파일 그룹에 배치됩니다. 이전 전체 텍스트 카탈로그 경로가 유효하지 않으면 업그레이드 과정에서 전체 텍스트 인덱스가 기본 테이블과 같은 파일 그룹에 유지되며, 테이블이 분할된 경우에는 주 파일 그룹에 유지됩니다.  
  
  
##  <a name="full-text-upgrade-options"></a><a name="FT_Upgrade_Options"></a> 전체 텍스트 업그레이드 옵션  
 서버 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드할 때 사용자 인터페이스를 통해 다음과 같은 전체 텍스트 업그레이드 옵션 중 하나를 선택할 수 있습니다.  
  
**가져오기**  
 전체 텍스트 카탈로그를 가져옵니다. 일반적으로 가져오기가 다시 작성보다 훨씬 빠릅니다. 예를 들어 CPU를 하나만 사용하는 경우 가져오기가 다시 작성보다 10배 정도 빠릅니다. 그러나 전체 텍스트 카탈로그를 가져오면 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 설치된 새 단어 분리기가 사용되지 않습니다. 쿼리 결과가 일관성이 유지되도록 하려면 전체 텍스트 카탈로그를 다시 작성해야 합니다.  
  
> [!NOTE]  
>  다시 작성은 다중 스레드 모드로 실행할 수 있으므로 CPU를 11개 이상 사용할 수 있는 경우 다시 작성에서 모든 CPU를 사용할 수 있게 설정하면 다시 작성이 가져오기보다 빠르게 실행될 수 있습니다.  
  
 전체 텍스트 카탈로그를 사용할 수 없는 경우 연결된 전체 텍스트 인덱스가 다시 작성됩니다. 이 옵션은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 대해서만 사용할 수 있습니다.  
  
 전체 텍스트 인덱스를 가져오는 데 따르는 영향에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "전체 텍스트 업그레이드 옵션 선택 시 고려 사항"을 참조하십시오.  
  
 **다시 빌드**  
 향상된 새로운 단어 분리기를 사용하여 전체 텍스트 카탈로그를 다시 작성합니다. 인덱스를 다시 작성하면 시간이 오래 걸릴 수 있으며 업그레이드 후 CPU 및 메모리가 많이 필요할 수 있습니다.  
  
 **재설정**  
 전체 텍스트 카탈로그를 다시 설정합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 업그레이드할 때는 전체 텍스트 카탈로그 파일이 제거되지만 전체 텍스트 카탈로그 및 전체 텍스트 인덱스의 메타데이터는 유지됩니다. 업그레이드가 끝나면 모든 전체 텍스트 인덱스의 변경 내용 추적이 해제되고 탐색이 자동으로 시작되지 않습니다. 업그레이드가 완료된 후 전체 채우기를 수동으로 실행할 때까지 카탈로그가 비어 있습니다.  
  
##  <a name="considerations-for-choosing-a-full-text-upgrade-option"></a><a name="Choosing_Upgade_Option"></a> 전체 텍스트 업그레이드 옵션 선택 시 고려 사항  
 업그레이드 옵션을 선택할 때는 다음 사항을 고려해야 합니다.  
  
-   쿼리 결과의 일관성을 보장하는 것은 중요한 일입니다.  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 전체 텍스트 및 의미 체계 검색에서 사용할 새로운 단어 분리기를 설치합니다. 단어 분리기는 인덱싱 및 쿼리 시에 모두 사용됩니다. 전체 텍스트 카탈로그를 다시 작성하지 않으면 검색 결과가 일관적이지 않을 수 있습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 단어 분리기와 현재 단어 분리기에서 다르게 분리되는 구를 찾는 전체 텍스트 쿼리를 실행하면 해당 구가 포함된 문서 또는 행이 검색되지 않을 수 있습니다. 그 이유는 인덱싱된 구가 현재 사용되는 쿼리와 다른 논리를 사용하여 분리되었기 때문입니다. 이를 해결하려면 인덱스 시 및 쿼리 시 동작이 동일하도록 새 단어 분리기를 사용하여 전체 텍스트 카탈로그를 다시 채우면(다시 작성하면) 됩니다. Rebuild 옵션을 선택하여 이 작업을 수행하거나 Import 옵션을 선택한 후 수동으로 다시 작성할 수 있습니다.  
  
-   정수 전체 텍스트 키 열에 작성된 전체 텍스트 인덱스가 있는지 여부  
  
     다시 작성할 때 내부 최적화가 수행되어 업그레이드된 전체 텍스트 인덱스의 쿼리 성능이 향상되는 경우가 있습니다. 특히 전체 텍스트 카탈로그에 기본 테이블의 전체 텍스트 키 열이 정수 데이터 형식인 전체 텍스트 인덱스가 있는 경우 다시 작성을 통해 업그레이드 후 전체 텍스트 쿼리의 성능을 극대화할 수 있습니다. 이러한 경우 **다시 작성** 옵션을 사용하는 것이 좋습니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 전체 텍스트 인덱스에서 전체 텍스트 키로 사용하는 열을 정수 데이터 형식으로 설정하는 것이 좋습니다. 자세한 내용은 [전체 텍스트 인덱스 성능 향상](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)을 참조하세요.  
  
-   서버 인스턴스를 온라인 상태로 만들기의 중요도  
  
     업그레이드 도중 가져오기나 다시 작성을 수행할 경우 CPU 리소스가 많이 사용되어 서버 인스턴스의 나머지 부분을 업그레이드하고 온라인 상태로 만드는 작업이 지연됩니다. 서버 인스턴스를 최대한 빨리 온라인 상태로 만들어야 하며 업그레이드 후 수동 채우기를 실행할 수 있는 경우 **다시 설정** 옵션이 적합합니다.  
  
## <a name="ensure-consistent-query-results-after-importing-a-full-text-index"></a>전체 텍스트 인덱스를 가져온 후 일관된 쿼리 결과 보장  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드할 때 전체 텍스트 카탈로그를 가져온 경우 이전 단어 분리기와 새 단어 분리기의 동작이 약간 다르므로 쿼리와 전체 텍스트 인덱스 내용이 일치하지 않을 수 있습니다. 이러한 경우 쿼리와 전체 텍스트 인덱스 내용이 완전히 일치하게 하려면 다음 옵션 중 하나를 선택합니다.  
  
-   전체 텍스트 인덱스가 들어 있는 전체 텍스트 카탈로그를 다시 작성([ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name* REBUILD)  
  
-   전체 텍스트 인덱스에 대해 FULL POPULATION 실행([ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ON *table_name* START FULL POPULATION)  
  
 단어 분리기에 대한 자세한 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)를 참조하세요.  
  
## <a name="upgrade-noise-word-files-to-stoplists"></a>의미 없는 단어 파일을 중지 목록으로 업그레이드  
데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]로 업그레이드하면 의미 없는 단어 파일이 더 이상 사용되지 않습니다. 그러나 이전에 사용된 의미 없는 단어 파일이 FTDATA\ FTNoiseThesaurusBak 폴더에 저장되므로 나중에 해당 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 중지 목록을 업데이트하거나 새로 작성할 때 사용할 수 있습니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 업그레이드한 후  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]설치에서 의미 없는 단어 파일을 추가, 수정 또는 삭제하지 않은 경우 시스템 중지 목록에서 사용자의 요구 사항을 충족해야 합니다.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 의미 없는 단어 파일이 수정되었으면 이러한 수정 사항은 업그레이드 동안 손실됩니다. 이러한 업데이트를 다시 만들려면 해당 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 중지 목록에서 이러한 수정 사항을 수동으로 다시 만들어야 합니다. 자세한 내용은 [ALTER FULLTEXT STOPLIST&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)를 참조하세요.  
  
-   전체 텍스트 인덱스에 아무 중지 단어도 적용하지 않으려면(예를 들어 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 설치에서 의미 없는 단어 파일을 삭제하거나 지운 경우) 업그레이드된 각 전체 텍스트 인덱스에 대해 중지 목록 설정을 해제해야 합니다. 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다( *database* 를 업그레이드된 데이터베이스의 이름으로 바꾸고 *table* 을 *table*이름으로 바꿈).  
  
    ```  
    Use database;   
    ALTER FULLTEXT INDEX ON table  
       SET STOPLIST OFF;  
    GO  
    ```  
  
     STOPLIST OFF 절은 중지 단어 필터링을 제거하고, 의미가 없는 것으로 간주되는 단어를 필터링하지 않고 테이블 채우기를 트리거합니다.  
  
## <a name="backup-and-imported-full-text-catalogs"></a>전체 텍스트 카탈로그 백업 및 가져오기  
 업그레이드 도중 다시 작성되거나 다시 설정된 전체 텍스트 카탈로그 및 새로 작성된 전체 텍스트 카탈로그는 논리적인 개념이며 파일 그룹에 존재하지 않습니다. 따라서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 전체 텍스트 카탈로그를 백업하려면 카탈로그의 전체 텍스트 인덱스가 들어 있는 파일 그룹을 모두 확인하여 하나씩 백업해야 합니다. 자세한 내용은 [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)을 참조하세요.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 가져온 전체 텍스트 카탈로그는 여전히 자체 파일 그룹의 데이터베이스 파일입니다. 전체 텍스트 카탈로그에 대한 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 의 백업 프로세스가 여전히 적용되지만 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에는 MSFTESQL 서비스가 없습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 프로세스에 대한 자세한 내용은 SQL Server 2005 온라인 설명서에서 [전체 텍스트 카탈로그 백업 및 복원](/previous-versions/sql/sql-server-2005/ms142511(v=sql.90)) 을 참조하세요.  
  
##  <a name="migrating-full-text-indexes-when-upgrading-a-database-to-sscurrent"></a><a name="Upgrade_Db"></a> 데이터베이스를 다음으로 업그레이드할 때 전체 텍스트 인덱스 마이그레이션: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 데이터베이스 연결, 복원 또는 복사 마법사를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만든 데이터베이스 파일 및 전체 텍스트 카탈로그를 기존 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 서버 인스턴스로 업그레이드할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 전체 텍스트 인덱스(있는 경우)는 가져오거나 다시 설정하거나 다시 작성할 수 있습니다. **upgrade_option** 서버 속성은 이러한 데이터베이스 업그레이드 도중 서버 인스턴스에서 사용할 전체 텍스트 업그레이드 옵션을 제어합니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 연결, 복원 또는 복사하면 데이터베이스를 바로 사용할 수 있으며 해당 데이터베이스가 자동으로 업그레이드됩니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 가져오기로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다.  
  
 **서버 인스턴스의 전체 텍스트 업그레이드 동작을 변경하려면**  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]: [sp\_fulltext\_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)의 **upgrade\_option** 동작을 사용합니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **:****서버 속성** 대화 상자의 **전체 텍스트 업그레이드 옵션** 을 사용합니다. 자세한 내용은 [서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)을 참조하세요.  
  
##  <a name="considerations-for-restoring-a-ssversion2005-full-text-catalog-to-sscurrent"></a><a name="Considerations_for_Restore"></a>[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 전체 텍스트 카탈로그를 다음으로 복원 시 고려 사항: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스의 전체 텍스트 데이터를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 로 업그레이드하는 방법 중 하나는 전체 데이터베이스 백업을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 복원하는 것입니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 전체 텍스트 카탈로그를 가져올 때 데이터베이스와 카탈로그 파일을 백업 및 복원할 수 있습니다. 이 동작은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]와 같습니다.  
  
-   전체 데이터베이스 백업에 전체 텍스트 카탈로그가 포함됩니다. 전체 텍스트 카탈로그를 참조하려면 해당 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 파일 이름인 sysft_+*catalog-name*을 사용합니다.  
  
-   전체 텍스트 카탈로그가 오프라인 상태이면 백업이 실패합니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 전체 텍스트 카탈로그 백업 및 복원에 대한 자세한 내용은 온라인 설명서에서 [전체 텍스트 카탈로그 백업 및 복원](./back-up-and-restore-full-text-catalogs-and-indexes.md) 및 [파일 백업과 복원 및 전체 텍스트 카탈로그](/previous-versions/sql/sql-server-2008-r2/ms190643(v=sql.105))[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 를 참조하세요.  
  
 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 복원하면 전체 텍스트 카탈로그에 대한 새 데이터베이스 파일이 만들어집니다. 이 파일의 기본 이름은 ftrow_*catalog-name*.ndf입니다. 예를 들어 *catalog-name* 이 `cat1`이면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스 파일의 기본 이름은 `ftrow_cat1.ndf`입니다. 대상 디렉터리에서 이 기본 이름이 이미 사용되고 있으면 새 데이터베이스 파일의 이름이 `ftrow_`*catalog-name*`{`*GUID*`}.ndf`로 지정됩니다. 여기에서 *GUID* 는 새 파일의 전역 고유 식별자입니다.  
  
 카탈로그를 가져온 후 **sys.database_files** 및 **sys.master_files**가 업데이트되어 카탈로그 항목이 제거되고 **sys.fulltext_catalogs** 의 **path** 열이 NULL로 설정됩니다.  
  
 **데이터베이스를 백업하려면**  
  
-   [전체 데이터베이스 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)(전체 복구 모델에만 해당)  
  
 **데이터베이스 백업을 복원하려면**  
  
-   [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
### <a name="example"></a>예제  
 [이라는](../../t-sql/statements/restore-statements-transact-sql.md) 데이터베이스를 복원하는 다음 예의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RESTORE `ftdb1`문에는 MOVE 절이 사용됩니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스, 로그 및 카탈로그 파일이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 서버 인스턴스에서 다음과 같은 새 위치로 이동합니다.  
  
-   데이터베이스 파일인 `ftdb1.mdf`는 `C:\Program Files\Microsoft SQL Server\MSSQL.1MSSQL13.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf`로 이동합니다.  
  
-   로그 파일인 `ftdb1_log.ldf`는 로그 디스크 드라이브의 로그 디렉터리인 *log_drive*`:\`*log_directory*`\ftdb1_log.ldf`로 이동합니다.  
  
-   `sysft_cat90` 카탈로그에 해당하는 카탈로그 파일은 `C:\temp`로 이동합니다. 가져온 전체 텍스트 인덱스는 데이터베이스 파일인 C:\ftrow_sysft_cat90.ndf에 자동으로 배치되고 C:\temp는 삭제됩니다.  
  
```  
RESTORE DATABASE [ftdb1] FROM  DISK = N'C:\temp\ftdb1.bak' WITH  FILE = 1,  
   MOVE N'ftdb1' TO N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf',  
    MOVE N'ftdb1_log' TO N'log_drive:\log_directory\ftdb1_log.ldf',  
    MOVE N'sysft_cat90' TO N'C:\temp';  
```  
  
##  <a name="attaching-a-sql-server-2005-database-to-sscurrent"></a><a name="Attaching_2005_ft_catalogs"></a> SQL Server 2005 데이터베이스를 다음에 연결: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 전체 텍스트 카탈로그는 전체 텍스트 인덱스의 그룹을 나타내는 논리적 개념입니다. 전체 텍스트 카탈로그는 어떠한 파일 그룹에도 속하지 않는 가상 개체입니다. 그러나 전체 텍스트 카탈로그 파일이 포함된 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 서버 인스턴스에 연결하면 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]의 경우와 같이 카탈로그 파일이 다른 데이터베이스 파일과 함께 이전 위치에서 연결됩니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 연결된 각 전체 텍스트 카탈로그의 상태는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 데이터베이스를 분리할 때의 상태와 같습니다. 분리 작업에 따라 전체 텍스트 인덱스 채우기가 일시 중지된 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 채우기가 재개되고 전체 텍스트 인덱스를 전체 텍스트 검색에 사용할 수 있게 됩니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 전체 텍스트 카탈로그 파일을 찾을 수 없거나 연결 작업 도중 전체 텍스트 파일이 이동했는데 새 위치가 지정되지 않은 경우의 동작은 선택한 전체 텍스트 업그레이드 옵션에 따라 다릅니다. 전체 텍스트 업그레이드 옵션이 **가져오기** 또는 **다시 작성**이면 연결된 전체 텍스트 카탈로그가 다시 작성됩니다. 전체 텍스트 업그레이드 옵션이 **다시 설정**이면 연결된 전체 텍스트 카탈로그가 다시 설정됩니다.  
  
 데이터베이스를 연결 및 분리하는 방법은 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md), [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md), [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) 및 [sp_detach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [전체 텍스트 검색 시작](../../relational-databases/search/get-started-with-full-text-search.md)   
 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [검색 필터 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
