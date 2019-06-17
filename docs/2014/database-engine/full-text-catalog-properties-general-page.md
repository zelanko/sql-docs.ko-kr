---
title: 전체 텍스트 카탈로그 속성 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.general.f1
ms.assetid: d1f66762-2d40-4f24-b635-a417d22ee79a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: be73ed98700ef261ccee026469dddd22017998e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779666"
---
# <a name="full-text-catalog-properties-general-page"></a>전체 텍스트 카탈로그 속성(일반 페이지)
  이 섹션에서는 **전체 텍스트 카탈로그 속성** 대화 상자의 **일반** 페이지에서 사용할 수 있는 옵션과 기능을 보여 줍니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 데이터베이스에서 전체 텍스트 카탈로그는 전체 텍스트 인덱스 그룹을 나타내는 논리적 개념입니다. 전체 텍스트 카탈로그는 어떠한 파일 그룹에도 속하지 않는 가상 개체입니다.  
  
## <a name="options"></a>변수  
  
### <a name="properties"></a>속성  
 **기본 카탈로그**  
 카탈로그가 데이터베이스의 기본 카탈로그인지 여부를 표시합니다.  
  
 **채우기 상태**  
 카탈로그의 상태를 나타냅니다. 가능한 값은  
  
-   **Idle**  
  
-   **탐색 진행 중**  
  
-   **일시 중지됨**  
  
-   **Throttled**  
  
-   **Recovering**  
  
-   **종료**  
  
-   **증분 채우기 진행 중**  
  
-   **인덱스 작성 중**  
  
-   **디스크는 전체 일시 중지**  
  
-   **Change tracking**  
  
 **항목 수**  
 카탈로그의 전체 텍스트 항목 수를 표시합니다.  
  
 **카탈로그 크기**  
 전체 텍스트 카탈로그의 크기(MB)를 표시합니다.  
  
 **이름**  
 전체 텍스트 카탈로그의 이름입니다.  
  
 **악센트 구분**  
 카탈로그에서 물결표( **~** ), 양음 악센트 표시(**´**) 또는 움라우트(**¨**) 등의 분음 기호를 구분할지 여부를 확인하거나 수정합니다. 유효한 값은  
  
-   **아니요**  
  
-   **예**  
  
-   분음 기호에 대 한 정보를 참조 하세요 [분음 부호](https://www.merriam-webster.com/dictionary/diacritic) Merriam Webster 사전에 있습니다.  
  
 **마지막 채우기 날짜**  
 마지막으로 카탈로그를 채운 날짜를 표시합니다.  
  
 **소유자**  
 전체 텍스트 카탈로그의 소유자입니다.  
  
 **고유 키 수**  
 카탈로그의 전체 텍스트 인덱스를 구성하는 고유한 단어 수입니다.  
  
### <a name="catalog-action"></a>카탈로그 동작  
  
|||  
|-|-|  
|**없음**|**카탈로그 최적화**, **카탈로그 다시 작성**또는 **카탈로그 다시 채우기** 작업을 수행하지 않습니다.|  
|**카탈로그 최적화**|카탈로그의 공간 사용률을 최적화하고 쿼리 성능을 향상시킵니다. 카탈로그를 최적화하면 검색 결과의 검색 순위 정확도도 향상됩니다.<br /><br /> 이 동작은 ALTER FULLTEXT CATALOG *catalog_name* REORGANIZE를 실행합니다.|  
|**카탈로그 다시 작성**|전체 텍스트 카탈로그를 삭제하고 다시 작성합니다. 악센트 구분과 같은 기본 카탈로그 속성이 변경된 경우에는 이 작업을 반드시 수행해야 합니다.<br /><br /> 카탈로그를 다시 작성하려면 전체 텍스트 카탈로그가 있는 파일 그룹이 온라인 상태 또는 읽고 쓸 수 있는 상태여야 합니다. 다시 작성 후 전체 텍스트 인덱스가 다시 채워집니다.<br /><br /> 이 동작은 ALTER FULLTEXT CATALOG *catalog_name* REBUILD를 실행합니다.|  
|**카탈로그 다시 채우기**|데이터의 최근 변경 내용을 적용하여 카탈로그를 업데이트합니다. 이 작업을 수행하는 동안에는 카탈로그를 사용하지 않아야 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 인덱스 채우기](../relational-databases/indexes/indexes.md)  
  
  
