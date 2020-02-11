---
title: 전체 텍스트 카탈로그 속성 (테이블 및 뷰 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.tablesviews.f1
ms.assetid: 2d45fcd2-0f0f-4167-9027-316d6696c106
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 78d7dc111bc0b6eb10e80f32785beeda710e52bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779194"
---
# <a name="full-text-catalog-properties-tables-and-views-page"></a>전체 텍스트 카탈로그 속성(테이블 및 뷰 페이지)
  이 대화 상자를 사용하여 전체 텍스트 카탈로그에 할당된 테이블과 뷰를 보거나 수정할 수 있습니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **이 데이터베이스에서 적합한 모든 테이블/뷰 개체**  
 고유 인덱스가 정의되어 있지만 아직 전체 텍스트 카탈로그에 포함되지 않은 테이블 및 뷰를 나열합니다. 테이블이 나 뷰를 선택 하 여 카탈로그에 할당 하려면 목록 상자에서 항목을 선택 하 고 "->" 단추를 누릅니다.  
  
 **카탈로그에 할당된 테이블/뷰 개체**  
 현재 전체 텍스트 카탈로그에 할당된 테이블과 뷰를 나열합니다.  
  
## <a name="selected-object-properties"></a>선택한 개체 속성  
 **선택한 개체 속성**  
 카탈로그에 할당된 개체 목록 상자에서 선택한 개체의 속성을 표시합니다.  
  
 **고유 인덱스**  
 테이블이나 뷰에 사용할 수 있는 고유 인덱스를 나열합니다.  
  
 **테이블에서 전체 텍스트 사용**  
 테이블에서 전체 텍스트 인덱스를 사용하려면 이 확인란을 선택합니다. 전체 텍스트 인덱스를 사용하지 않으려면 이 확인란의 선택을 취소합니다.  
  
## <a name="eligible-columns-grid"></a>적합한 열 표  
  
|||  
|-|-|  
|**사용 가능한 열**|전체 텍스트 인덱싱된 모든 열을 표시합니다. 전체 텍스트 인덱스에 열을 추가하려면 확인란을 선택합니다.|  
|**단어 분리기 용 언어**|단어 분리기의 언어를 표시합니다.|  
|**데이터 형식 열**|열이 `varbinary(max)` 또는 `image` 열인 경우 **사용 가능한 열** 에 나열 된 열의 문서 유형을 포함 하는 테이블의 열 이름을 나열 합니다.|  
|**통계 의미 체계**|선택한 열에 대해 의미 체계 인덱싱을 사용하도록 설정할지 여부를 선택합니다. 자세한 내용은 [의미 체계 검색&#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md)을 참조하세요.<br /><br /> 
  **통계 의미 체계** 를 선택하기 전에 **언어**를 선택했으며 선택한 언어에 연결된 의미 체계 언어 모델이 없으면 **통계 의미 체계** 확인란은 사용할 수 없습니다. 
  **언어** 를 선택하기 전에 **통계 의미 체계**를 선택한 경우 드롭다운 콤보 상자에서 사용할 수 있는 언어가 의미 체계 언어 모델에서 지원하는 언어로 제한됩니다.|  
  
## <a name="track-changes"></a>변경 내용 추적  
  
|||  
|-|-|  
|**자동**|기본 테이블의 데이터가 수정, 추가 또는 삭제되면 전체 텍스트 인덱스가 자동으로 업데이트됩니다.|  
|**수동**|인덱싱된 데이터가 수정, 추가 또는 삭제되면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 변경 내용을 추적합니다. 
  **수동** 변경 내용 추적을 사용하는 경우 해당 변경 내용으로 인덱스가 자동으로 업데이트되지 않습니다. 대신 관리자가 [ALTER FULLTEXT INDEX ... START UPDATE POPULATION](/sql/t-sql/statements/alter-fulltext-index-transact-sql) 문을 사용하여 수동으로 변경 내용을 적용할 수 있습니다.|  
|**변경 내용 추적 안 함**|이 옵션을 사용하는 경우 카탈로그의 인덱싱된 데이터에 대한 변경 내용이 기록되지 않습니다. 관리자는 ALTER FULLTEXT INDEX와 함께 FULL POPULATION 또는 INCREMENTAL POPULATION을 사용하여 인덱스를 만들어야 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;전체 텍스트 카탈로그 만들기](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [ALTER FULLTEXT CATALOG&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [전체 텍스트 인덱스 채우기](../relational-databases/indexes/indexes.md)  
  
  
