---
title: "R에서 OLAP 큐브의 데이터 사용 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# R에서 OLAP 큐브의 데이터 사용

**olapR** 패키지는 Microsoft R Server 및 SQL Server R Services에서 제공되는 새로운 R 패키지로, 이 패키지를 통해 MDX 쿼리를 실행하고 R 솔루션에서 OLAP 큐브의 데이터를 사용할 수 있습니다.

이 패키지를 사용하면 연결된 서버를 만들거나 일반 행 집합을 정리할 필요가 없으며 R에서 직접 OLAP 데이터를 사용할 수 있습니다.

## <a name="overview"></a>개요

OLAP 큐브는 *측정값*을 통해 미리 계산된 집계를 포함하는 다차원 데이터베이스이며, 일반적으로 판매액, 판매 개수 또는 기타 숫자 값과 같은 중요한 비즈니스 메트릭을 캡처합니다. OLAP 큐브는 시간에 따라 중요한 비즈니스 데이터를 캡처하고 저장하는 데 광범위하게 사용됩니다. OLAP 데이터는 다양한 도구, 대시보드 및 시각화에서 비즈니스 분석에 사용됩니다. 자세한 내용은 [Online analytical processing](https://en.wikipedia.org/wiki/Online_analytical_processing)(온라인 분석 처리)을 참조하세요.

**olapR** 패키지는 MDX 쿼리를 만드는 두 가지 방법을 지원합니다. 

- R 스타일 API를 사용하여 큐브, 축 및 슬라이서를 선택하면 간단한 MDX 쿼리를 생성할 수 있습니다. 이러한 함수를 사용하면 기존의 OLAP 도구에 액세스할 수 없거나 MDX 언어에 대한 깊은 지식이 없어도 유효한 MDX 쿼리를 작성할 수 있습니다.

  MDX는 매우 복잡할 수 있기 때문에 일부 MDX 쿼리는 **olapR** 패키지에서 이 방법을 사용하여 만들지 못할 수도 있습니다. 그러나 N 차원에서 조각화, 분석, 드릴다운, 롤업, 피벗 등 가장 일반적이고 유용한 모든 작업을 지원합니다.

+ 모든 MDX 쿼리는 수동으로 만든 다음 붙여 넣을 수 있습니다. 이 옵션은 다시 사용하려는 기존 MDX 쿼리가 있는 경우 또는 작성하려는 쿼리가 너무 복잡하여 **olapR**에서 처리할 수 없는 경우에 유용합니다. 

  이 접근 방식에서는 SSMS 또는 Excel과 같은 클라이언트 유틸리티를 사용하여 MDX를 작성한 후 이 패키지에서 제공하는 *SSAS 쿼리 처리기*에 대한 문자열 인수로 사용합니다. **olapR** 함수는 지정된 Analysis Services 서버로 쿼리를 보내고 결과를 R에 다시 전달합니다.

MDX 쿼리를 작성하거나 기존 MDX 쿼리를 실행하는 방법에 대한 예는 [R을 사용하여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)을 참조하세요.


## <a name="mdx-basics"></a>MDX 기본 사항

큐브의 데이터는 MDX(MultiDimensional Expression) 쿼리 언어를 사용하여 검색할 수 있습니다. OLAP 큐브(또는 Analysis Services 데이터베이스)의 데이터는 테이블 형식이 아니라 다차원이기 때문에 MDX는 데이터를 필터링하고 조각화하기 위해 복잡한 구문 및 다양한 작업을 지원합니다.

+ *조각화* 한 차원에 대한 값을 선택하여 한 차원 더 작은 큐브를 생성하는 방식으로 큐브의 하위 집합을 사용합니다. 

+ *분할* 여러 차원에서 값의 범위를 지정하여 하위 큐브를 만듭니다.

+ *드릴다운* 요약에서 세부 정보로 탐색합니다.

+ *드릴업* 세부 정보에서 더 높은 수준의 집계로 이동합니다.

+ *롤업* 한 차원에 데이터를 요약합니다.

+ *피벗* 큐브 또는 데이터 선택을 회전합니다.

이 항목에서는 큐브를 쿼리하는 기본 구문을 보여 주는 추가 예제를 제공합니다.
[R을 사용하여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)


## <a name="known-issues"></a>알려진 문제

### <a name="tabular-models-not-supported-currently"></a>현재 테이블 형식 모델이 지원되지 않음

Analysis Services의 테이블 형식 인스턴스에 연결할 수 있고 `explore` 함수는 TRUE 반환 값과 함께 성공을 보고하지만 테이블 형식 모델 개체가 호환되는 형식이 아니며 탐색할 수 없습니다. 

테이블 형식 모델은 MDX 쿼리를 지원하지만 테이블 형식 모델에 대한 MDX 쿼리는 NULL 결과를 반환하고 오류를 보고하지 않습니다.

## <a name="resources"></a>리소스

OLAP 또는 MDX 쿼리를 처음 사용하는 경우 Wikipedia 문서 [OLAP Cubes](https://en.wikipedia.org/wiki/OLAP_cube)(OLAP 큐브)
[MDX queries](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)(MDX 쿼리)를 참조하세요.

### <a name="samples"></a>샘플

큐브에 대해 자세히 알아보려면 Analysis Services 자습서의 4단원 [OLAP 큐브 만들기](https://msdn.microsoft.com/library/ms170208.aspx)까지 수행하여 이러한 예제에서 사용되는 큐브를 만들 수 있습니다.

기존 큐브를 백업으로 다운로드하여 Analysis Services의 인스턴스로 복원할 수도 있습니다. 예를 들어 [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)(Adventure Works 다차원 모델 SQL 2014)의 완전히 처리된 큐브를 압축된 형식으로 다운로드하여 SSAS 인스턴스로 복원할 수 있습니다. 자세한 내용은 [백업 및 복원](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md), 또는 [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
[R을 사용하여 MDX 쿼리를 만드는 방법](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

[Analysis Services MDX 쿼리 디자이너](Analysis%20Services%20MDX%20Query%20Designer%20User%20Interface%20\(Report%20Builder\).md)

