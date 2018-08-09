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
ms.openlocfilehash: d9657b1433b0647d7165cb427da6333c0a325583
ms.sourcegitcommit: 0cda14b1151d9bce1253d96dea038c038484f07a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39400926"
---
#<a name="appliance-feature-switch"></a>어플라이언스 기능 스위치
합니다 **기능 스위치가** 페이지 분석 플랫폼 시스템 2016-AU7 도입 된 두 개의 기능 스위치에 대 한 정보가 표시 됩니다. 이 페이지를 사용 하 여 업데이트 하거나 기능 및 Analytics Platform System에 대 한 설정을 설정/해제 합니다. 기능 스위치 값을 변경 서비스를 다시 시작을 해야 합니다.

![DWConig 어플라이언스 기능 스위치가](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 어플라이언스 기능 스위치") 

##<a name="autostatsenabled-switch"></a>AutoStatsEnabled 스위치
자동 통계 기능을 제어합니다. 이 기능 스위치가 설정 된 AU7로 업그레이드 한 후 기본적으로 true입니다. 업그레이드 후에 만든 모든 데이터베이스는 자동 생성 및 비동기 통계 업데이트에 상속 됩니다. 기존 데이터베이스에 대 한 데이터베이스 관리자가 사용 하 여 자동 통계를 설정할 수 있습니다 [ALTER DATABASE (병렬 데이터 웨어하우스)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)합니다. 통계에 대 한 자세한 내용은 참조 하세요. [통계](../relational-databases/statistics/statistics.md)합니다.

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>DmsProcessStopMessageTimeoutInSeconds 스위치
데이터 이동을 포함 하는 쿼리에서 취소 되 면 사용 중인 시스템 동기화 하기 위해 데이터 이동 서비스 (DMS) 대기 시간을 제어 합니다. 900 초 (15 분)을 기본적으로이 값을 설정 AU7로 업데이트 합니다. 유효한 범위는 0에서 3600 초입니다.
