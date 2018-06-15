---
title: 위젯에 대 한 정보를 사용 하 여 서버와 SQL 작업 Studio (미리 보기)에서 데이터베이스를 모니터링할 | Microsoft Docs
description: SQL 작업 Studio (미리 보기)에 대 한 정보 위젯을에 대해 알아봅니다.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article"
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77f34ceebb4f02c829b2df3efcae5e64c2eaa1bf
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235932"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>서버 및에 대 한 정보 위젯 사용 하 여 데이터베이스 관리 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

통찰력 위젯을 사용할 서버 및 데이터베이스를 사용 하면 TRANSACT-SQL (T-SQL) 쿼리 및 통찰력 시각화로 전환 합니다. 

Insights는 사용자 지정할 수 있는 차트 및 서버 및 데이터베이스 모니터링 대시보드를 추가 하는 그래프입니다. 서버와 데이터베이스의에서 요약 정보 보기 다음 자세한 세부 정보를 검색 하 고 정의 하는 관리 작업을 시작 합니다. 

놀라운 서버 및 데이터베이스 관리 대시보드는 다음 예제와 비슷한 빌드할 수 있습니다.

![데이터베이스 대시보드](media/insight-widgets/database-dashboard.png)


에 이동 하 고 다양 한 유형의 통찰력 위젯 만들기를 시작 하려면 다음 자습서 확인해 보세요.

- [사용자 지정 통찰력 위젯 빌드](tutorial-build-custom-insight-sql-server.md)
- *기본 제공 통찰력 위젯 사용*
   - [성능 모니터링 정보를 사용 하도록 설정](tutorial-qds-sql-server.md)
   - [테이블 공간 사용량 정보를 사용 하도록 설정](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 쿼리 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 다른 언어 또는 작업이 너무 많은 사용자 인터페이스 T-SQL 가능한 한 최소한의 JSON 구성으로 사용 하려고 시도 하므로 아직 시 키 지 않도록 하려고 시도 합니다. T-SQL을 사용 하 여 통찰력 위젯 구성 통찰력 위젯으로 변환할 수 있는 유용한 T-SQL 쿼리의 기존 원본 무수 한 수를 활용 합니다.

하나 또는 두 개의 T-SQL 쿼리 통찰력 위젯 구성 되어 있습니다.
* *통찰력 위젯 쿼리* , 필수 이며 위젯에서 표시 되는 데이터를 반환 하는 쿼리입니다.
* *세부 정보 쿼리 통찰력* 은 통찰력 세부 정보 페이지를 만드는 경우에 필요 합니다.

통찰력 위젯 쿼리 수, 차트 또는 그래프를 렌더링 하는 데이터 집합을 정의 합니다. 통찰력 세부 정보 쿼리를 사용 하 여 통찰력 세부 정보 창에서 테이블 형식에 대 한 관련 정보 세부 정보를 나열 합니다. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 통찰력 위젯 쿼리를 실행 하 고 차트의 데이터 집합에 쿼리 결과 집합에 매핑합니다 다음 렌더링 합니다. 사용자가 insight의 세부 정보를 열면 통찰력 세부 정보 쿼리를 실행 하 고 대화 상자 내에서 표 보기에서 결과 출력 합니다.

기본 개념 개수, 차트 및 그래프 위젯의 데이터 집합으로 사용할 수 있도록 방식으로 T-SQL 쿼리를 작성 하는 것입니다. 

## <a name="summary"></a>요약

T-SQL 쿼리 및 결과 집합 통찰력 위젯 동작을 결정합니다. 차트 종류에 대 한 쿼리를 작성 하거나 기존 쿼리는 오른쪽 차트 종류를 매핑하는 효과적인 통찰력 위젯 만들려는 주요 고려 사항인입니다.



## <a name="additional-resources"></a>추가 리소스
- [쿼리 편집기](tutorial-sql-editor.md)

