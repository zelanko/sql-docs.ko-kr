---
title: 사용 또는 사용 현황 데이터 수집을 사용 하지 않도록 설정 하 고 크래시 SQL 작업 Studio (미리 보기)에 대 한 보고 | Microsoft Docs
description: 이 문서에는 사용 및 충돌 보고 데이터를 수집 하 고 Microsoft로 전송 하는 경우를 제어 하는 방법을 설명 합니다.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fbf952360599642497c1d7109229cba89728d61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>에 대 한 사용 데이터 컬렉션 설정 또는 해제 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>원격 분석 보고를 해제 하는 방법

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 사용 현황 데이터를 수집 하 고 자사 제품 및 서비스를 개선 하는 Microsoft로 보냅니다. 자세한 내용을 보려면 읽고는 [개인정보취급방침](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)합니다.

Microsoft 사용 현황 데이터를 전송 하려는 하지 않는 경우 설정할 수 있습니다는 *telemetry.enableTelemetry* 설정을 *false*합니다.

무음에서 모든 원격 분석 이벤트를 [!INCLUDE[name-sos](../includes/name-sos-short.md)]에서 **파일** > **기본 설정** > **설정을**, 다음 옵션을 추가 합니다.

```json
    "telemetry.enableTelemetry": false
```

**중요 알림**:이 옵션의 다시 시작이 필요한 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 내용이 적용 됩니다. 

## <a name="how-to-disable-crash-reporting"></a>충돌 보고를 해제 하는 방법

충돌 보고를 해제 하려면에서 **파일** > **기본 설정** > **설정을**, 다음 옵션을 추가 합니다.

```json
    "telemetry.enableCrashReporter": false
```

**중요 알림**:이 옵션의 다시 시작이 필요한 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 내용이 적용 됩니다.

## <a name="additional-resources"></a>추가 리소스
- [작업 영역 및 사용자 설정](settings.md)