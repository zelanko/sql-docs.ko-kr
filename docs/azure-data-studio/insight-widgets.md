---
title: Azure Data Studio에서 인사이트 위젯을 사용하여 서버 및 데이터베이스 모니터링
titleSuffix: Azure Data Studio
description: Azure Data Studio의 인사이트 위젯에 대해 알아보기
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.openlocfilehash: c1ab90efa97878676b1adc2a62579527407d6ba6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959520"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)]에서 인사이트 위젯을 사용하여 서버 및 데이터베이스 관리

인사이트 위젯은 서버 및 데이터베이스를 모니터링하는 데 T-SQL(Transact-SQL) 쿼리를 사용하며 이 쿼리를 인사이트를 제공하는 시각화로 변환합니다.

인사이트는 서버 및 데이터베이스 모니터링 대시보드에 추가하는 사용자 지정 가능한 차트 및 그래프입니다. 서버 및 데이터베이스의 인사이트 요약을 보고, 추가 세부 정보를 자세히 살펴보고, 정의한 관리 작업을 시작합니다.

다음 예제와 비슷한 멋진 서버 및 데이터베이스 관리 대시보드를 빌드할 수 있습니다.

![데이터베이스 대시보드](media/insight-widgets/database-dashboard.png)


다양한 유형의 인사이트 위젯 만들기를 시작하려면 다음 자습서를 확인하세요.

- [사용자 지정 인사이트 위젯 빌드](tutorial-build-custom-insight-sql-server.md)
- *기본 제공 인사이트 위젯 사용*
  - [성능 모니터링 인사이트 사용](tutorial-qds-sql-server.md)
  - [테이블 공간 사용량 인사이트 사용](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>SQL 쿼리

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 다른 언어나 과도하게 사용되는 사용자 인터페이스 도입을 피하려고 하므로 최소한의 JSON 구성을 통해 T-SQL을 최대한 많이 사용하려고 합니다. T-SQL을 사용하여 인사이트 위젯을 구성하면 인사이트를 제공하는 위젯으로 변환할 수 있는 유용한 T-SQL 쿼리의 수많은 기존 원본을 활용할 수 있습니다.

인사이트 위젯은 하나 또는 두 개의 T-SQL 쿼리로 구성됩니다.
* ‘인사이트 위젯 쿼리’는 필수이며 위젯에 표시되는 데이터를 반환하는 쿼리입니다. 
* ‘인사이트 세부 정보 쿼리’는 인사이트 세부 정보 페이지를 만드는 경우에만 필요합니다. 

인사이트 위젯 쿼리는 개수, 차트 또는 그래프를 렌더링하는 데이터 세트를 정의합니다. 인사이트 세부 정보 쿼리는 인사이트 세부 정보 패널에서 관련 인사이트 세부 정보를 테이블 형식으로 나열하는 데 사용됩니다. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 인사이트 위젯 쿼리를 실행하고 쿼리 결과 세트를 차트의 데이터 세트에 매핑한 후 렌더링합니다. 사용자가 인사이트 세부 정보를 열면 인사이트 세부 정보 쿼리가 실행되고 결과가 대화 상자 내의 그리드 보기로 출력됩니다.

기본 개념은 개수, 차트 및 그래프 위젯의 데이터 세트로 사용할 수 있도록 하는 방식으로 T-SQL 쿼리를 작성하는 것입니다. 

## <a name="summary"></a>요약

T-SQL 쿼리와 그 결과 세트에 따라 인사이트 위젯 동작이 결정됩니다. 차트 종류에 대한 쿼리를 작성하거나 기존 쿼리에 적합한 차트 종류를 매핑하는 것은 효과적인 인사이트 위젯을 빌드하기 위한 주요 고려 사항입니다.



## <a name="additional-resources"></a>추가 리소스
- [쿼리 편집기](tutorial-sql-editor.md)

