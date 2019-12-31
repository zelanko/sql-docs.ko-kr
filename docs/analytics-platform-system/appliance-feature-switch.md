---
title: 기능 스위치
description: 분석 플랫폼 시스템 AU7에 도입 된 두 가지 기능 스위치에 대 한 정보를 표시 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 8642f27a329da8819acf0ab99a648c4979ed40d0
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401450"
---
# <a name="appliance-feature-switches"></a>어플라이언스 기능 스위치

**기능 스위치** 페이지에는 Analytics PLATFORM System AU7 이상에서 도입 된 기능 스위치에 대 한 정보가 표시 됩니다. 이 구성 페이지를 사용 하 여 분석 플랫폼 시스템의 기능 및 설정을 업데이트 하거나 사용 하지 않도록 설정할 수 있습니다.

> [!NOTE]
> 기능 스위치 값을 변경 하려면 서비스를 다시 시작 해야 합니다.

![DWConfig 어플라이언스 기능 스위치](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConfig 어플라이언스 기능 스위치")

## <a name="autostatsenabled"></a>AutoStatsEnabled

자동 통계 기능을 제어 합니다. AU7로 업그레이드 한 후이 기능 스위치는 기본적으로 true로 설정 됩니다. 업그레이드 후에 생성 된 모든 데이터베이스는 통계의 자동 생성 및 비동기 업데이트를 상속 합니다. 기존 데이터베이스의 경우 데이터베이스 관리자는 [ALTER database (병렬 데이터 웨어하우스)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)를 사용 하 여 자동 통계를 설정할 수 있습니다. 통계에 대 한 자세한 내용은 [통계](../relational-databases/statistics/statistics.md)를 참조 하세요.

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries

삽입/선택 작업에 대해 1 보다 큰 maxdop 설정을 선택할 수 있습니다. 이 설정에 대 한 옵션은 0, 1, 2 및 4 이며 기본값은 1입니다.

## <a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions

SQL 쿼리 최적화 프로그램에서 일반적인 하위 식에 대 한 데이터 이동을 제거 하 여 쿼리 성능을 향상 시킵니다. 이 기능에 대 한 자세한 설명은 [여기](common-sub-expression-elimination.md)를 참조 하십시오.

## <a name="usecatalogqueries"></a>UseCatalogQueries

SMO를 사용 하는 대신 일부 메타 데이터 호출에 대해 카탈로그 개체를 사용 하는 경우 성능 향상이 표시 됩니다. CU 7.1에서는 기본적으로 true로 설정 합니다 .이 스위치는 해당 동작을 제어 합니다.

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds

데이터 이동 관련 쿼리를 취소할 때 DMS (데이터 이동 서비스)가 사용 중인 시스템에서 동기화를 대기 하는 시간을 제어 합니다. AU7로 업데이트 하면이 값은 기본적으로 900 초 (15 분)로 설정 됩니다. 유효한 범위는 0-3600 초입니다.
