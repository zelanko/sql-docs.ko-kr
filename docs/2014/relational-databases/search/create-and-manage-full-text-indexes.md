---
title: 전체 텍스트 인덱스 만들기 및 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a41f11b200ffe5dfc91479ea54095fd24c90699a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011552"
---
# <a name="create-and-manage-full-text-indexes"></a>전체 텍스트 인덱스 만들기 및 관리
  전체 텍스트 인덱스의 정보는 전체 텍스트 엔진이 테이블에서 특정 단어나 단어 조합을 빠르게 검색할 수 있는 전체 텍스트 쿼리를 컴파일하는 데 사용됩니다. 전체 텍스트 인덱스는 하나 이상의 데이터베이스 테이블 열에 중요한 단어와 그 위치에 대한 정보를 저장합니다. 전체 텍스트 인덱스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 전체 텍스트 엔진이 작성하고 유지 관리하는 특수한 유형의 토큰 기반 인덱스입니다. 전체 텍스트 인덱스의 작성 과정은 다른 유형의 인덱스를 작성하는 것과 다릅니다. 특정 행에 저장된 값을 기준으로 B-트리 구조를 생성하는 대신 전체 텍스트 엔진은 인덱싱되는 텍스트의 개별 토큰을 기준으로 반전된 누적 압축 인덱스 구조를 작성합니다.  전체 텍스트 인덱스 크기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되는 컴퓨터의 사용 가능한 메모리 리소스에 의해서만 제한됩니다.  
  
 전체 텍스트 인덱스는 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 파일 시스템에 있었던 것과는 달리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]부터는 데이터베이스 엔진과 통합됩니다. 새 데이터베이스에서 전체 텍스트 카탈로그는 어떤 파일 그룹에도 속하지 않는 가상 개체이며, 전체 텍스트 인덱스의 그룹을 나타내는 논리적인 개념일 뿐입니다. 그러나 데이터 파일이 들어 있는 전체 텍스트 카탈로그인 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스를 업그레이드하는 동안에는 새 파일 그룹이 만들어집니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](upgrade-full-text-search.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 전체 텍스트 엔진이 별도의 서비스가 아닌 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 있습니다. 전체 텍스트 엔진을 데이터베이스 엔진에 통합하면 전체 텍스트 관리 효율성, 혼합 쿼리의 최적화 및 전체 성능이 향상됩니다.  
  
 테이블당 한 개의 전체 텍스트 인덱스만 허용합니다. 테이블에 대한 전체 텍스트 인덱스를 만들려면 해당 테이블에 Null이 아닌 고유한 단일 열이 있어야 합니다. `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, `varbinary` 형식의 열에 대해 전체 텍스트 인덱스를 만들 수 있으며 `varbinary(max)`를 전체 텍스트 검색의 인덱스로 사용할 수도 있습니다. 데이터 형식이 `varbinary`, `varbinary(max)`, `image` 또는 `xml`인 열에 대한 전체 텍스트 인덱스를 만들려면 유형 열을 지정해야 합니다. *유형 열* 은 각 행에 있는 문서의 파일 확장명(.doc, .pdf, .xls 등)이 저장되는 테이블 열입니다.  
  
 전체 텍스트 인덱스를 만들고 유지 관리하는 과정을 *채우기* (또는 *탐색*)라고 합니다. 전체 텍스트 인덱스 채우기에는 전체 채우기, 변경 내용 추적 기반 채우기 및 증분 타임스탬프 기반 채우기의 세 가지가 있습니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](populate-full-text-indexes.md)를 참조하세요.  
  
##  <a name="tasks"></a> 일반 작업  
 **전체 텍스트 인덱스를 만들려면**  
  
-   [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **전체 텍스트 인덱스를 변경 하려면**  
  
-   [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **전체 텍스트 인덱스를 삭제 하려면**  
  
-   [DROP FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)  
  
 [항목 내용](#top)  
  
##  <a name="structure"></a> 전체 텍스트 인덱스 구조  
 전체 텍스트 인덱스의 구조를 잘 알게 되면 전체 텍스트 엔진의 작동 원리를 이해하는 데 도움이 됩니다. 이 항목에서 예제 테이블로 사용하는 테이블은 **의** Document [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 테이블에서 발췌한 것입니다. 이 테이블에는 **DocumentID** 열 및 **Title** 열의 2개 열과 테이블의 3개 행만 표시됩니다.  
  
 이 예에서는 **Title** 열에 대해 전체 텍스트 인덱스를 만들었다고 가정합니다.  
  
|DocumentID|Title|  
|----------------|-----------|  
|1|Crank Arm and Tire Maintenance|  
|2|Front Reflector Bracket and Reflector Assembly 3|  
|3|Front Reflector Bracket Installation|  
  
 예를 들어 조각 1을 보여 주는 아래 표에서는 **Document** 테이블의 **Title** 열에 생성된 전체 텍스트 인덱스의 내용을 설명합니다. 전체 텍스트 인덱스에는 이 표에 표시되어 있는 것보다 많은 정보가 포함되어 있습니다. 이 표는 전체 텍스트 인덱스를 논리적으로 표현한 것이며 설명 목적으로만 제공됩니다. 행은 디스크 사용률을 최적화하기 위해 압축된 형식으로 저장됩니다.  
  
 데이터는 원래 문서와 다르게 반전되었습니다. 왜냐하면 키워드가 문서 ID로 매핑되기 때문입니다. 따라서 전체 텍스트 인덱스를 반전된 인덱스라고 부르기도 합니다.  
  
 또한 전체 텍스트 인덱스에서 "and" 키워드가 제거되었습니다. 왜냐하면 "and"가 중지 단어이고 전체 텍스트 인덱스에서 중지 단어를 제거하면 디스크 공간이 크게 절약되어 쿼리 성능을 높일 수 있기 때문입니다. 중지 단어에 대한 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
 **조각 1**  
  
|키워드|ColId|DocId|발생 빈도|  
|-------------|-----------|-----------|----------------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|유지 관리|1|1|5|  
|Front|1|2|1|  
|Front|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Bracket|1|3|3|  
|어셈블리|1|2|6|  
|3|1|2|7|  
|설치|1|3|4|  
  
 **Keyword** 열에는 인덱싱할 때 추출한 단일 토큰이 표시됩니다. 토큰을 구성하는 요소는 단어 분리기에 의해 결정됩니다.  
  
 **ColId** 열에는 전체 텍스트 인덱싱된 특정 열에 해당하는 값이 포함됩니다.  
  
 `DocId` 열 전체 텍스트 인덱싱된 테이블의 특정 전체 텍스트 키 값에 매핑되는 8 바이트 정수에 대 한 값을 포함 합니다. 이 매핑은 전체 텍스트 키가 정수 데이터 형식이 아닌 경우에만 필요합니다. 이러한 경우 전체 텍스트 간의 매핑을 키 값 및 `DocId` 값 DocId Mapping 테이블 이라는 개별 테이블에 유지 됩니다. 이러한 매핑을 쿼리하려면 [sp_fulltext_keymappings](/sql/relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql) 시스템 저장 프로시저를 사용합니다. 검색 조건을 충족하려면 위 테이블의 DocId 값이 쿼리 중인 기본 테이블에서 행을 검색할 수 있도록 DocId Mapping 테이블과 조인되어야 합니다. 기본 테이블의 전체 텍스트 키 값이 정수 형식인 경우 값은 DocId로 직접 사용되며 매핑이 필요하지 않습니다. 따라서 정수 전체 텍스트 키 값을 사용하면 전체 텍스트 쿼리 최적화에 도움이 될 수 있습니다.  
  
 **Occurrence** 열에는 정수 값이 포함됩니다. 각 DocId 값에는 해당 DocId 내의 특정 키워드에 대한 상대적 단어 오프셋에 해당하는 발생 빈도 값의 목록이 있습니다. 발행 빈도 값은 구 또는 근접 단어 일치를 확인하는 데 유용합니다. 예를 들어 구는 발생 빈도 값의 숫자가 서로 인접해 있습니다. 발생 빈도 값은 관련성을 평가하는 데에도 유용합니다. 예를 들어 DocId의 키워드 발생 빈도를 평가 시 사용할 수 있습니다.  
  
 [항목 내용](#top)  
  
##  <a name="fragments"></a> 전체 텍스트 인덱스 조각  
 논리적 전체 텍스트 인덱스는 일반적으로 여러 개의 내부 테이블로 분할됩니다. 이러한 각 내부 테이블을 전체 텍스트 인덱스 조각이라고 부릅니다. 이러한 조각 중 일부는 비교적 최신의 데이터를 포함할 수도 있습니다. 예를 들어 사용자가 DocId가 3인 다음 행을 업데이트하고 테이블에서 자동으로 변경 내용이 추적되는 경우 새로운 조각이 만들어집니다.  
  
|DocumentID|Title|  
|----------------|-----------|  
|3|Rear Reflector|  
  
 다음 예제에서 조각 2에 포함된 DocId 3 관련 데이터는 조각 1에 포함된 데이터에 비해 새로운 데이터입니다. 따라서 사용자가 "Rear Reflector"를 쿼리하면 조각 2의 데이터가 DocId 3에 대해 사용됩니다. 각 조각은 생성 타임스탬프로 구분되며 이 타임스탬프는 [sys.fulltext_index_fragments](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql) 카탈로그 뷰를 사용하여 쿼리할 수 있습니다.  
  
 **조각 2**  
  
|키워드|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Rear|1|3|1|  
|Reflector|1|3|2|  
  
 조각 2에서 볼 수 있듯이 전체 텍스트 쿼리에서는 각 조각을 내부적으로 쿼리하고 이전 항목을 무시해야 합니다. 따라서 전체 텍스트 인덱스에 전체 텍스트 인덱스 조각이 너무 많으면 쿼리 성능이 크게 저하될 수 있습니다. 조각 수를 줄이려면 [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 REORGANIZE 옵션을 사용하여 전체 텍스트 카탈로그를 다시 구성합니다. 이 문은 *마스터 병합*을 수행하고 이 병합에서는 여러 조각을 하나의 큰 조각으로 병합하고 전체 텍스트 인덱스에서 사용되지 않는 항목을 모두 제거합니다.  
  
 다시 구성 작업 후 예제 인덱스에는 다음과 같은 행이 포함됩니다.  
  
|키워드|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|유지 관리|1|1|5|  
|Front|1|2|1|  
|Rear|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|어셈블리|1|2|6|  
|3|1|2|7|  
  
 [항목 내용](#top)  
  
  
