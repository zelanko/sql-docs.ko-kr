---
title: 테이블 자동 조인
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: a98ac8db359d4e47911ce3a2ca97b6cdd5494d90
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011704"
---
# <a name="join-tables-automatically-visual-database-tools"></a>테이블 자동 조인(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
쿼리에 두 개 이상의 테이블을 추가하면 [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 가 해당 테이블 사이의 관련성을 판단합니다. 관련이 있는 경우 쿼리 및 뷰 디자이너는 테이블 또는 테이블 구조 개체를 나타내는 사각형 사이에 자동으로 조인 선을 넣습니다.  
  
다음과 같은 경우 쿼리 및 뷰 디자이너는 테이블이 조인되었다고 판단합니다.  
  
-   데이터베이스에 테이블 관련성을 지정하는 정보가 포함된 경우  
  
-   이름과 데이터 형식이 같은 두 개의 열이 각 테이블에 하나씩 있는 경우. 이 열은 하나 이상의 테이블에서 기본 키여야 합니다. 예를 들어, `employee` 와 `jobs` 테이블을 추가하고 `job_id` 열이 `jobs` 테이블의 기본 키이며 각 테이블에 데이터 형식이 같은 `job_id` 라는 열이 있는 경우 쿼리 및 뷰 디자이너는 이 두 테이블을 자동으로 조인합니다.  
  
    > [!NOTE]  
    > 쿼리 및 뷰 디자이너는 이름과 데이터 형식이 같은 열을 기반으로 하여 조인을 하나만 만듭니다. 둘 이상의 조인이 가능한 경우에도 쿼리 및 뷰 디자이너는 처음 발견한 일치 열 집합을 기반으로 해서 하나의 조인을 만든 다음 조인 작업을 중단합니다.  
  
-   쿼리 및 뷰 디자이너에서 검색 조건(WHERE 절)이 실제 조인 조건임을 감지하는 경우. 예를 들어, `employee` 및 `jobs`테이블을 추가한 다음 두 테이블의 `job_id` 열에서 같은 값을 검색하는 검색 조건을 만들 수 있습니다. 이때 쿼리 및 뷰 디자이너는 검색 조건의 결과로 조인이 만들어짐을 감지하여 검색 조건을 기반으로 해서 조인 조건을 만듭니다.  
  
쿼리 및 뷰 디자이너가 사용자 쿼리에 적합하지 않은 조인을 만든 경우 조인을 수정하거나 제거할 수 있습니다. 자세한 내용은 [조인 연산자 수정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md) 및 [조인 제거&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-joins-visual-database-tools.md)를 참조하세요.  
  
쿼리 및 뷰 디자이너가 사용자 쿼리에 있는 테이블을 자동으로 조인하지 않는 경우 사용자가 직접 조인을 만들 수 있습니다. 자세한 내용은 [테이블 수동 조인&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자이너의 조인 표시 방법&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/how-the-query-and-view-designer-represents-joins-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[조인을 사용한 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
