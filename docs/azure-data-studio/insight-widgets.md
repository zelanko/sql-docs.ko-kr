---
title: Azure Data Studio의 정보 위젯을 사용 하 여 서버 및 데이터베이스 모니터링
titleSuffix: Azure Data Studio
description: Azure Data Studio에 대 한 정보 위젯 알아보기
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: jroth
ms.openlocfilehash: 1be7f5b9fdc53f013908dc22464c28cbc219bd78
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795576"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>서버 및 데이터베이스에 대 한 정보 위젯 사용 하 여 관리 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

정보 위젯 서버 및 데이터베이스를 사용 하면 TRANSACT-SQL (T-SQL) 쿼리를 수행할 통찰력 시각화로 전환 하 고 있습니다.

Insights는 사용자 지정 가능한 차트 및 대시보드를 모니터링 하는 데이터베이스 서버를 추가 하는 그래프입니다. 서버 및 데이터베이스에서 요약 정보 보기 하 고 자세한 세부 정보를 정의 하는 관리 작업을 시작 합니다.

멋진 서버 및 데이터베이스 관리 대시보드는 다음 예제와 비슷한를 빌드할 수 있습니다.

![데이터베이스 대시보드](media/insight-widgets/database-dashboard.png)


시작 하 고 다양 한 유형의 정보 위젯 만들기를 시작 하려면 다음 자습서를 확인해 보세요.

- [빌드 사용자 지정 정보 위젯](tutorial-build-custom-insight-sql-server.md)
- *기본 제공 정보 위젯 사용*
  - [성능 모니터링 정보를 사용 하도록 설정](tutorial-qds-sql-server.md)
  - [테이블 공간 사용량 정보를 사용 하도록 설정](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 쿼리

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 다른 언어 또는 많은 사용자 인터페이스 최소 JSON 구성을 사용 하 여 최대한 많은 T-SQL을 사용 하려고 하므로 아직 추가 되지 않도록 하려고 합니다. T-SQL을 사용 하 여 정보 위젯 구성 수많은 기존 원본 통찰력 있는 위젯에 설정할 수 있는 유용한 T-SQL 쿼리의 수가 활용 합니다.

하나 또는 두 개의 T-SQL 쿼리 정보 위젯 구성 되어 있습니다.
* *정보 위젯 쿼리* 필수 이며 위젯에 표시 되는 데이터를 반환 하는 쿼리.
* *Insight 세부 정보 쿼리* 는 insight 세부 정보 페이지를 만드는 경우에 필요 합니다.

정보 위젯 쿼리를 개수, 차트 또는 그래프를 렌더링 하는 데이터 집합을 정의 합니다. Insight 세부 정보 쿼리를 사용 하 여 insight 세부 정보 창에서 테이블 형식으로 정보를 관련 된 정보를 나열 하 합니다. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] insigh 위젯 쿼리를 실행 하 고 차트의 데이터 집합 쿼리 결과 집합 매핑되 렌더링 합니다. 사용자가 정보 활용의 세부 정보를 열면 insight 세부 정보 쿼리를 실행 하 고 대화 상자에서 그리드 보기에서 결과 출력 합니다.

기본 개념 수, 차트 및 그래프 위젯의 데이터 집합으로 사용할 수 있도록 방식으로 T-SQL 쿼리를 작성 하는 것입니다. 

## <a name="summary"></a>요약

T-SQL 쿼리 및 해당 결과 집합 정보 위젯 동작을 결정 합니다. 차트 종류에 대 한 쿼리를 작성 하거나 기존 쿼리에 대 한 오른쪽 차트 종류를 매핑하기는 효과적인 통찰력 위젯을 빌드할 주요 고려 사항인 경우



## <a name="additional-resources"></a>추가 리소스
- [쿼리 편집기](tutorial-sql-editor.md)

