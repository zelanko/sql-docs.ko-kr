---
title: 기능 스위치가 (분석 플랫폼 시스템)
description: 분석 플랫폼 시스템 AU7에 도입 된 두 개의 기능 스위치에 대 한 정보를 표시 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e384a252584fed0e7543a7a4000fc9a70f6533e7
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550904"
---
#<a name="appliance-feature-switch"></a>어플라이언스 기능 스위치
**기능 스위치가** 페이지 분석 플랫폼 시스템 AU7에 도입 된 두 개의 기능 스위치에 대 한 정보를 표시 합니다. 이 페이지를 사용 하 여를 업데이트 하거나 기능 및 설정을 분석 플랫폼 시스템에 설정/해제 합니다. 기능 스위치 값을 변경 하려면 서비스를 다시 시작 합니다.

![DWConig 기기 기능 스위치가](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 어플라이언스 기능 스위치가") 

##<a name="autostatsenabled-switch"></a>AutoStatsEnabled 스위치
자동 통계 기능을 제어합니다. 이 기능 스위치가로 설정 되어 AU7로 업그레이드 한 후 기본적으로 true입니다. 업그레이드 후에 만든 모든 데이터베이스는 자동 생성 및 비동기 업데이트 통계를 상속 합니다. 기존 데이터베이스에 대 한 데이터베이스 관리자가 사용 하도록 설정할 수 있는 통계 자동 [데이터베이스 변경] (/ sql/t-sql/statements/alter-database-parallel-data-warehouse). 통계에 대 한 자세한 내용은 참조 하십시오. [통계](../relational-databases/statistics/statistics.md)합니다.

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>DmsProcessStopMessageTimeoutInSeconds 스위치
데이터 이동 서비스 (DMS) 데이터를 이동 하는 쿼리 취소 되 면 사용량이 많은 시스템에 동기화 할 때까지 대기 시간을 제어 합니다. 900 초 (15 분)를 기본적으로이 값을 설정 AU7를 업데이트 합니다. 유효한 범위는 0에서 3600 초입니다.
