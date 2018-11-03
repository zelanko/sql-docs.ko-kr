---
title: 기능 스위치 (분석 플랫폼 시스템)
description: 분석 플랫폼 시스템 AU7에 도입 된 두 개의 기능 스위치에 대 한 정보를 표시 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 0d2aadb0e7c0c56c69d89bc94e0ddaacef54e837
ms.sourcegitcommit: 3e1efbe460723f9ca0a8f1d5a0e4a66f031875aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50236909"
---
#<a name="appliance-feature-switches"></a>어플라이언스 기능 스위치
합니다 **기능 스위치가** 페이지 분석 플랫폼 시스템 AU7 이상 도입 되는 기능 스위치에 대 한 정보가 표시 됩니다. 이 구성 페이지를 사용 하 여 업데이트 하거나 기능 및 Analytics Platform System에 대 한 설정을 설정/해제 합니다. 기능 스위치 값 변경에는 서비스를 다시 시작을 해야합니다.

![DWConig 어플라이언스 기능 스위치가](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 어플라이언스 기능 스위치") 

##<a name="autostatsenabled"></a>AutoStatsEnabled
자동 통계 기능을 제어합니다. 이 기능 스위치가 설정 된 AU7로 업그레이드 한 후 기본적으로 true입니다. 업그레이드 후에 만든 모든 데이터베이스는 자동 생성 및 비동기 통계 업데이트에 상속 됩니다. 기존 데이터베이스에 대 한 데이터베이스 관리자가 사용 하 여 자동 통계를 설정할 수 있습니다 [ALTER DATABASE (병렬 데이터 웨어하우스)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)합니다. 통계에 대 한 자세한 내용은 참조 하세요. [통계](../relational-databases/statistics/statistics.md)합니다.

##<a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries
Insert/select 작업에 대해 1 보다 큰 maxdop 설정을 선택할 수 있습니다. 이 설정에 대 한 옵션 0, 1, 2, 4, 기본값은 1 이며

##<a name="usecatalogqueries"></a>UseCatalogQueries
카탈로그 개체를 사용 하 여 SMO를 사용 하는 대신 일부 메타 데이터 호출에 대 한 향상을 된 성능을 보여 주었습니다. 해당 동작을 제어 하는 CU7.1,이 스위치에에서는 기본적으로 true로 설정 합니다. 

##<a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds
데이터 이동을 포함 하는 쿼리에서 취소 되 면 사용 중인 시스템 동기화 하기 위해 데이터 이동 서비스 (DMS) 대기 시간을 제어 합니다. 900 초 (15 분)을 기본적으로이 값을 설정 AU7로 업데이트 합니다. 유효한 범위는 0에서 3600 초입니다.