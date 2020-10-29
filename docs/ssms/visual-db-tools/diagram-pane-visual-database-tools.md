---
description: 다이어그램 창(Visual Database Tools)
title: 다이어그램 창
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: eaba2d8acd2a0443bfe2ed97fc53b50fcb667629
ms.sourcegitcommit: fb8724fb99c46ecf3a6d7b02a743af9b590402f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2020
ms.locfileid: "92439387"
---
# <a name="diagram-pane-visual-database-tools"></a>다이어그램 창(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
다이어그램 창은 데이터 연결에서 선택한 테이블 또는 테이블 반환 개체를 그래픽으로 표시합니다. 또한 이들 사이의 조인 관계도 보여 줍니다.  
  
다이어그램 창에서는 다음 작업을 수행할 수 있습니다.  
  
-   테이블과 테이블 반환 개체를 추가하거나 제거하고 출력할 데이터 열을 지정합니다.  
  
-   테이블과 테이블 반환 개체 간에 조인을 만들거나 수정합니다.  
  
다이어그램 창의 내용을 변경하면 조건 창과 SQL 창에 변경 내용이 반영되어 업데이트됩니다. 예를 들어, 다이어그램 창의 테이블 또는 테이블 반환 개체 창에서 출력할 열을 선택하면 쿼리 및 뷰 디자이너는 조건 창과 SQL 창의 SQL 문에 데이터 열을 추가합니다.  
  
각 테이블 또는 테이블 반환 개체는 다이어그램 창에서 별도의 창으로 나타납니다. 각 사각형의 제목 표시줄에 있는 아이콘은 다음 표에서 설명하는 바와 같이 사각형이 나타내는 개체 형식을 보여 줍니다.  
  
## <a name="options"></a>옵션  
**테이블**  
다이어그램 창에 추가할 수 있는 테이블을 나열합니다. 테이블을 추가하려면 테이블을 선택하고 **추가** 를 클릭합니다. 여러 테이블을 한번에 추가하려면 원하는 테이블을 모두 선택하고 **추가** 를 클릭합니다.  
  
**Views**  
다이어그램 창에 추가할 수 있는 뷰를 나열합니다. 뷰를 추가하려면 뷰를 선택하고 **추가** 를 클릭합니다. 여러 뷰를 한번에 추가하려면 원하는 뷰를 모두 선택하고 **추가** 를 클릭합니다.  
  
**함수**  
다이어그램 창에 추가할 수 있는 사용자 정의 함수를 나열합니다. 함수를 추가하려면 함수를 선택하고 **추가** 를 클릭합니다. 여러 함수를 한번에 추가하려면 원하는 함수를 모두 선택하고 **추가** 를 클릭합니다.  
  
**로컬 테이블**  
데이터베이스에 속한 테이블 대신 쿼리로 만든 테이블을 나열합니다.  
  
**동의어**  
다이어그램 창에 추가할 수 있는 동의어를 나열합니다. 동의어를 추가하려면 동의어를 선택하고 **추가** 를 클릭합니다. 여러 동의어를 한번에 추가하려면 원하는 동의어를 모두 선택하고 **추가** 를 클릭합니다.  
  
|아이콘|개체 유형|  
|--------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi1.gif":::|테이블|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi2.gif":::|쿼리 또는 뷰|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi3.gif":::|연결된 테이블|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dvudficon.gif":::|사용자 정의 함수|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi5.gif":::|연결된 뷰|  
  
각 사각형은 테이블 또는 테이블 반환 개체에 대한 데이터 열을 표시합니다. 열 이름 옆에는 확인란과 기호가 표시되어 쿼리에서 열이 사용되는 방법을 보여 줍니다. 도구 설명에서는 데이터 형식, 열 크기 등의 정보를 표시합니다.  
  
다음 표에는 각 테이블 또는 테이블 반환 개체의 사각형에서 사용하는 확인란 및 기호가 나열되어 있습니다.  
  
|확인란 또는 기호|설명|  
|-----------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi7.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi8.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi9.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbia.gif":::|데이터 열을 쿼리 결과 집합(선택 쿼리)에 나타낼지 또는 업데이트, 삽입 원본, 테이블 만들기 또는 삽입 위치 쿼리에서 사용할지 여부를 지정합니다. 열을 선택하여 결과에 추가합니다. **(모든 열)** 을 선택하면 모든 데이터 열이 출력에 나타납니다.<br /><br />확인란과 함께 사용하는 아이콘은 만드는 쿼리 형식에 따라 변경됩니다. 삭제 쿼리를 만들 때에는 열을 개별적으로 선택할 수 없습니다.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbib.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbic.gif":::|데이터 열이 ORDER BY 절의 일부인 쿼리 결과를 정렬하는 데 사용되고 있음을 나타냅니다. 정렬 순서가 오름차순이면 아이콘이 A-Z로 나타나고 내림차순이면 Z-A로 나타납니다.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbid.gif":::|데이터 열이 집계 쿼리에서 GROUP BY 절의 일부인 그룹화된 결과 집합을 만드는 데 사용되고 있음을 나타냅니다.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbie.gif":::|데이터 열이 WHERE 또는 HAVING 절의 일부인 쿼리에 대한 검색 조건에 포함되어 있음을 나타냅니다.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbif.gif":::|데이터 열의 내용이 SUM, AVG 또는 기타 집계 함수에 포함되어 있는 출력에 맞게 요약되고 있음을 나타냅니다.|  
  
> [!NOTE]  
> 테이블 또는 테이블 반환 개체에 대한 충분한 액세스 권한이 없거나 데이터베이스 드라이버가 이에 대한 정보를 반환하지 않으면 쿼리 및 뷰 디자이너에 데이터 열이 표시되지 않습니다. 이 경우 쿼리 및 뷰 디자이너는 테이블 또는 테이블 구조 개체의 제목 표시줄만 표시합니다.  
  
## <a name="joined-tables-on-the-diagram-pane"></a>다이어그램 창의 조인된 테이블  
쿼리에 조인이 포함되어 있으면 조인에 관련된 데이터 열 사이에 조인 선이 나타납니다. 예를 들어, 테이블 또는 테이블 반환 개체 창이 최소화되거나 조인에 식이 포함되어 조인된 데이터 열이 표시되지 않는 경우 쿼리 및 뷰 디자이너는 테이블 또는 테이블 반환 개체를 나타내는 사각형의 제목 표시줄에 조인 선을 표시합니다. 쿼리 및 뷰 디자이너는 각 조인 조건에 대해 한 개의 조인 선을 표시합니다.  
  
조인 선의 가운데 있는 아이콘 모양은 테이블 또는 테이블 구조 개체가 조인되는 방법을 보여 줍니다. 조인 절이 등호(=)가 아닌 연산자를 사용하는 경우 조인 선 아이콘에 해당 연산자가 표시됩니다. 다음 표는 조인 선에 표시될 수 있는 아이콘 목록입니다.  
  
|조인 선 아이콘|설명|  
|------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbih.gif":::|등호를 사용하여 만든 내부 조인|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbii.gif":::|">" 연산자를 기반으로 하는 내부 조인 조인 선 아이콘에 표시되는 연산자는 조인에 사용한 연산자를 나타냅니다.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbij.gif":::|관련 테이블에 일치하는 내용이 없는 경우에도 왼쪽에 나타난 테이블의 모든 행을 포함하는 외부 조인|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbik.gif":::|관련 테이블에 일치하는 내용이 없는 경우에도 오른쪽에 나타난 테이블의 모든 행을 포함하는 외부 조인|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbil.gif":::|관련 테이블에 일치하는 내용이 없는 경우에도 양쪽 테이블의 모든 행을 포함하는 완전 외부 조인|  
  
조인 선 끝에 있는 아이콘은 조인 형식을 나타냅니다. 다음 표는 조인 선 끝에 표시될 수 있는 조인 형식 및 아이콘 목록입니다.  
  
|조인 선 끝의 아이콘|설명|  
|-----------------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbim.gif":::|일 대 일 조인|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbin.gif":::|일 대 다 조인|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbio.gif ":::|쿼리 및 뷰 디자이너는 조인 형식을 결정할 수 없습니다.|  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[조건 창&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
