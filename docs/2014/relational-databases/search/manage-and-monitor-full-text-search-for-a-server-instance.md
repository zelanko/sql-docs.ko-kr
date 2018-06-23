---
title: 서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], about
- full-text search [SQL Server], server management
ms.assetid: 2733ed78-6d33-4bf9-94da-60c3141b87c8
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0631b46f507fa7cd3d106a28df686728055a94bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181044"
---
# <a name="manage-and-monitor-full-text-search-for-a-server-instance"></a>서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링
  서버 인스턴스의 전체 텍스트 관리에는 다음이 포함됩니다.  
  
-   FDHOST Launcher 서비스(MSSQLFDLauncher) 관리, 서비스 계정 자격 증명을 변경하는 경우 필터 데몬 호스트 프로세스 다시 시작, 서버 차원의 전체 텍스트 속성 구성, 전체 텍스트 카탈로그 백업 등의 시스템 관리 태스크. 예를 들어 서버 수준에서 전반적으로 서버 인스턴스의 기본 언어와 다른 기본 전체 텍스트 언어를 지정할 수 있습니다.  
  
-   전체 텍스트 언어 구성 요소 구성(단어 분리기, 형태소 분석기, 동의어 사전 파일, 중지 단어 및 중지 목록).  
  
-   전체 텍스트 검색에 대한 사용자 데이터베이스 구성. 여기에는 데이터베이스에 대해 하나 이상의 전체 텍스트 카탈로그를 만들고 전체 텍스트 쿼리를 실행할 각 테이블 또는 인덱싱된 뷰에 대한 전체 텍스트 인덱스를 정의하는 작업이 포함됩니다.  
  
##  <a name="props"></a> 전체 텍스트 검색의 서버 속성 보기 또는 변경  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]인스턴스의 전체 텍스트 속성을 볼 수 있습니다.  
  
#### <a name="to-view-and-change-server-properties-for-full-text-search"></a>전체 텍스트 검색의 서버 속성을 보고 변경하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **서버 속성** 대화 상자에서 **고급** 페이지를 클릭하여 전체 텍스트 검색에 대한 서버 정보를 봅니다. 전체 텍스트 속성은 다음과 같습니다.  
  
    -   **기본 전체 텍스트 언어**  
  
         전체 텍스트 인덱싱된 열에 대한 기본 언어를 지정합니다. 전체 텍스트 인덱싱된 데이터의 언어 분석은 데이터의 언어에 따라 달라집니다. 이 옵션의 기본값은 서버의 언어입니다. 표시되는 설정에 해당하는 언어에 대한 자세한 내용은 [sys.fulltext_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)를 참조하세요.  
  
    -   **전체 텍스트 업그레이드 옵션**  
  
         이 서버 속성은 데이터베이스를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 에서 이후 버전으로 업그레이드할 때 전체 텍스트 인덱스를 마이그레이션하는 방법을 제어합니다. 이 속성은 데이터베이스 복사 마법사를 사용하여 데이터베이스를 연결하거나, 데이터베이스 백업 및 파일 백업을 복원하거나, 데이터베이스를 복사하여 업그레이드에 적용됩니다.  
  
         대체 방법은 다음과 같습니다.  
  
         **가져오기**  
         전체 텍스트 카탈로그를 가져옵니다. 일반적으로 가져오기가 다시 작성보다 훨씬 빠릅니다. 예를 들어 CPU를 하나만 사용하는 경우 가져오기가 다시 작성보다 10배 정도 빠릅니다. 그러나 가져온 전체 텍스트 카탈로그에는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에 새로 도입된 향상된 단어 분리기가 사용되지 않으므로 결국에는 전체 텍스트 카탈로그를 다시 작성해야 할 수 있습니다.  
  
        > [!NOTE]  
        >  다시 작성은 다중 스레드 모드로 실행할 수 있으므로 CPU를 11개 이상 사용할 수 있는 경우 다시 작성에서 모든 CPU를 사용할 수 있게 설정하면 다시 작성이 가져오기보다 빠르게 실행될 수 있습니다.  
  
         전체 텍스트 카탈로그를 사용할 수 없는 경우 연결된 전체 텍스트 인덱스가 다시 작성됩니다. 이 옵션은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 데이터베이스에 대해서만 사용할 수 있습니다.  
  
         **Rebuild**  
         향상된 새로운 단어 분리기를 사용하여 전체 텍스트 카탈로그를 다시 작성합니다. 인덱스를 다시 작성하면 시간이 오래 걸릴 수 있으며 업그레이드 후 CPU 및 메모리가 많이 필요할 수 있습니다.  
  
         **다시 설정**  
         전체 텍스트 카탈로그를 다시 설정합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 전체 텍스트 카탈로그 파일이 제거되지만 전체 텍스트 카탈로그 및 전체 텍스트 인덱스의 메타데이터는 유지됩니다. 업그레이드가 끝나면 모든 전체 텍스트 인덱스의 변경 내용 추적이 해제되고 탐색이 자동으로 시작되지 않습니다. 업그레이드가 완료된 후 전체 채우기를 수동으로 실행할 때까지 카탈로그가 비어 있습니다.  
  
         전체 텍스트 업그레이드 옵션을 선택 하는 방법에 대 한 내용은 [전체 텍스트 검색 업그레이드](upgrade-full-text-search.md)합니다.  
  
        > [!NOTE]  
        >  [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)**upgrade_option** 동작을 사용하여 전체 텍스트 업그레이드 옵션을 설정할 수도 있습니다.  
  
##  <a name="metadata"></a> 추가 전체 텍스트 서버 속성 보기  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 함수를 사용하여 전체 텍스트 검색의 다양한 서버 수준 속성 값을 가져올 수 있습니다. 이 정보는 전체 텍스트 검색을 관리하고 이러한 검색에서 발생하는 문제를 해결하는 데 유용합니다.  
  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 인스턴스의 전체 텍스트 속성 및 관련 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 함수를 보여 줍니다.  
  
|속성|Description|기능|  
|--------------|-----------------|--------------|  
|`IsFullTextInstalled`|전체 텍스트 구성 요소가 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 설치되어 있는지 여부를 나타냅니다.|[FULLTEXTSERVICEPROPERTY](/sql/t-sql/functions/fulltextserviceproperty-transact-sql)<br /><br /> [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql)|  
|`LoadOSResources`|운영 체제 단어 분리기 및 필터가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와 함께 등록되고 사용되는지 여부를 나타냅니다.|FULLTEXTSERVICEPROPERTY|  
|`VerifySignature`|전체 텍스트 엔진이 서명된 이진 파일만 로드할지 여부를 지정합니다.|FULLTEXTSERVICEPROPERTY|  
  
##  <a name="monitor"></a> 전체 텍스트 검색 작업 모니터링  
 일부 동적 관리 뷰 및 함수는 서버 인스턴스의 전체 텍스트 검색 작업을 모니터링하는 데 유용합니다.  
  
 **채우기 작업이 진행 중인 전체 텍스트 카탈로그에 대한 정보를 보려면**  
  
-   [sys.dm_fts_active_catalogs&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql)  
  
 **필터 데몬 호스트 프로세스의 현재 작업을 보려면**  
  
-   [sys.dm_fts_fdhosts&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql)  
  
 **진행 중인 인덱스 채우기에 대한 정보를 보려면**  
  
-   [sys.dm_fts_index_population&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)  
  
 **전체 텍스트 탐색이나 전체 텍스트 탐색 범위의 일부로 사용되는 메모리 풀의 메모리 버퍼를 보려면**  
  
-   [sys.dm_fts_memory_buffers&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)  
  
 **전체 텍스트 탐색이나 전체 텍스트 탐색 범위에 대해 전체 텍스트 Gatherer 구성 요소에서 사용할 수 있는 공유 메모리 풀을 보려면**  
  
-   [sys.dm_fts_memory_pools&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)  
  
 **각 전체 텍스트 인덱싱 일괄 처리에 대한 정보를 보려면**  
  
-   [sys.dm_fts_outstanding_batches&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql)  
  
 **진행 중인 채우기와 관련된 특정 범위에 대한 정보를 보려면**  
  
-   [sys.dm_fts_population_ranges&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql)  
  
  
