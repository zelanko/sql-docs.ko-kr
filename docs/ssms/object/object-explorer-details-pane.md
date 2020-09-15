---
description: 개체 탐색기 세부 정보 창
title: 개체 탐색기 세부 정보 창
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.general.f1
- sql13.swb.summary.report.f1
helpviewer_keywords:
- object search [SQL Server], Object Explorer
- Object Explorer
- object search [SQL Server]
- searching objects [SQL Server]
ms.assetid: b963e3c2-dc9e-4d38-bd28-2e00fe9e0e47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c9ee38de46d4bcd689c471eb9f32fa79df40fa68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88370789"
---
# <a name="object-explorer-details-pane"></a>개체 탐색기 세부 정보 창
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 구성 요소인 개체 탐색기 정보는 서버의 모든 개체를 테이블 형식으로 표시하고 이러한 개체를 관리하기 위한 사용자 인터페이스를 제공합니다. 개체 탐색기의 기능은 서버의 유형에 따라 조금씩 다르지만 일반적으로 데이터베이스를 위한 개발 기능과 모든 서버 유형을 위한 관리 기능을 포함합니다.  
  
개체 탐색기 정보 창은 기본적으로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에 표시됩니다. 개체 탐색기가 표시되지 않으면 **보기** 메뉴에서 **개체 탐색기 정보** 를 클릭하거나 **F7**키를 누릅니다.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 가 시작될 때 사용되는 Microsoft Windows 국가 및 언어 옵션의 날짜 형식에 따라 날짜를 표시합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 다시 시작하면 새 설정이 반영됩니다.  
  
## <a name="object-explorer-details"></a>개체 탐색기 정보  
개체 탐색기 정보를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 폴더 및 개체를 탐색할 수 있습니다. 32비트 운영 체제에서는 개체 탐색기가 64,000개의 개체만 표시할 수 있습니다. 추가 개체에 액세스하려면 아이콘을 선택해야 합니다.  
  
개체 탐색기 정보에는 다음 표에 설명된 아이콘이 있는 도구 모음이 포함되어 있습니다. 아이콘은 해당되는 경우에만 사용할 수 있습니다.  
  
|아이콘|작업|  
|--------|----------|  
|**뒤로**|개체 탐색기 정보에 표시된 이전 항목으로 이동합니다. 이전 화면이 검색 작업으로 인한 결과 화면인 경우 검색을 다시 실행합니다.|  
|**앞으로**|**뒤로** 작업을 선택한 후 다음 화면으로 이동합니다.|  
|**위로**|부모 개체 또는 폴더로 이동합니다.|  
|**동기화**|개체 탐색기의 포커스를 개체 탐색기 정보에서 선택한 개체로 설정합니다.|  
|**Filter**|사용 가능한 경우 구성 가능한 개체 하위 집합을 표시합니다.|  
|**새로 고침**|개체 탐색기 정보의 화면 표시를 새로 고칩니다.|  
|**검색**|특정 데이터베이스 개체를 찾기 위한 검색 단어를 입력할 영역을 제공합니다.|  
  
### <a name="column-header-selections"></a>열 머리글 선택  
개체 탐색기 정보에는 선택할 수 있는 열이 있습니다. 열 머리글을 마우스 오른쪽 단추로 클릭하고 표시할 항목을 선택할 수 있습니다. 선택한 항목은 다른 개체를 탐색할 때도 그대로 유지됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 닫고 다시 시작해도 각 사용자가 선택한 설정이 그대로 유지됩니다.  
  
> [!CAUTION]  
> 데이터베이스와 같은 일부 개체 유형에 대한 열을 모두 표시하면 큰 개체 집합에 대한 표시 렌더링이 약간 느려질 수 있습니다.  
  
### <a name="sorting"></a>정렬  
열 머리글을 한 번 클릭하면 해당 열을 기준으로 정렬됩니다. 동일한 머리글을 다시 클릭하면 해당 열을 기준으로 역순으로 정렬됩니다. 각 사용자가 선택한 정렬 설정은 다른 개체 및 폴더에서도 그대로 유지되며 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 다시 시작해도 그대로 유지됩니다.  
  
### <a name="filtering"></a>필터링  
개체 탐색기 정보에 표시되는 특정 개체 목록은 개체 탐색기 정보 도구 모음의 **필터** 아이콘을 사용하여 필터링할 수 있습니다. 필터링이 가능하면 아이콘이 활성화됩니다.  
  
### <a name="details-pane"></a>정보 창  
개체 탐색기 정보의 맨 아래 영역에는 선택한 개체에 대한 특정 정보가 표시되는 패널이 있습니다. 여러 개체를 선택한 경우 개체 수만 표시됩니다. 패널에서 항목을 선택하고 **복사** 아이콘을 클릭하면 표시된 텍스트가 클립보드에 복사됩니다.  
  
아래쪽 화살표 키를 누르면 목록에서 다음 항목이 선택됩니다. 위쪽 화살표 키를 누르면 목록에서 이전 항목이 선택됩니다. 화살표 키를 누르고 있으면 항목 간 이동 속도가 빨라집니다. 속성 목록의 맨 아래 또는 맨 위 항목에서 선택이 중지됩니다.  
  
속성 이름의 첫 번째 문자를 입력하면 해당 문자로 시작하는 다음 속성이 선택됩니다.  
  
속성이 여러 열에 정렬되어 있는 경우 왼쪽 화살표 및 오른쪽 화살표 키를 사용하여 인접 열로 이동합니다.  
  
속성 값을 클립보드로 복사하려면 다음과 같은 키보드 키 조합을 사용합니다.  
  
-   Ctrl+C는 속성 값을 복사합니다.  
  
-   Ctrl+Shift+C는 탭 구분 기호를 사용하여 속성 이름과 속성 값을 복사합니다.  
  
개체 탐색기 정보 속성 창에서 오른쪽 클릭 메뉴를 사용하여 모든 속성 또는 모든 속성과 이름을 클립보드로 복사합니다.  
  
필드 너비가 좁아서 속성 값을 완전히 표시할 수 없을 때 속성 값을 표시하려면 마우스 커서를 값 위에 놓거나 속성 값에 UI 포커스를 설정하여 전체 속성 값이 들어 있는 도구 설명을 활성화합니다. 긴 속성 값에 포커스가 있으면 내게 필요한 옵션 화면 판독기가 전체 속성 값을 보고합니다.  
  
속성 창의 속성 수가 콘텐츠 영역에 표시될 수 있는 수보다 많으면 속성 창의 오른쪽에 스크롤 막대가 표시됩니다. 스크롤 막대를 사용하여 콘텐츠 영역의 속성 값 뷰를 조정할 수 있습니다.  
  
### <a name="multiple-object-selection"></a>여러 개체 선택  
개체 탐색기 정보에서는 여러 개체를 선택할 수 있습니다. 예를 들어 개체 탐색기에서 테이블을 선택하는 경우 개체 탐색기 정보 창에서 **Ctrl** 키를 누른 채 여러 테이블을 선택하고 마우스 오른쪽 단추를 클릭한 다음 **삭제** 또는 **테이블 스크립팅** 을 선택하여 선택한 모든 테이블에 대해 동시에 동작을 수행할 수 있습니다. 표준 복사 명령은 표시된 텍스트를 클립보드에 복사합니다.  
  
## <a name="sql-server-object-search"></a>SQL Server 개체 검색  
와일드카드  
  
-   표준 와일드카드 문자를 사용할 수 있습니다. 예를 들어 **dm_os%counters** 를 검색하면 dm_os_memory_cache_counters와 dm_os_performance_counters가 모두 반환됩니다. 자세한 내용은 [방법: 와일드 카드로 검색](../../relational-databases/scripting/search-text-with-wildcards.md)을 참조하세요.  
  
검색 범위  
  
-   각 검색의 범위는 개체 탐색기 트리의 현재 포커스로 한정됩니다. 예를 들어 데이터베이스에 개체 탐색기 포커스가 있는 경우 **dm_os%counters** 를 검색하면 해당 데이터베이스에서 dm_os_memory_cache_counters와 dm_os_performance_counters가 반환됩니다. 데이터베이스 노드에 개체 탐색기 포커스가 있는 경우 모든 데이터베이스가 검색되어 동적 뷰의 여러 인스턴스가 반환됩니다.  
  
큰 집합  
  
-   큰 개체 집합을 검색하면 시간이 많이 걸리고 서버 성능이 저하될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[개체 탐색기](../../ssms/object/object-explorer.md)  
  
