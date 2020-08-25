---
title: 사용량 현황 데이터 수집 및 크래시 보고 사용 또는 사용 안 함
description: 이 문서에서는 사용량 및 충돌 보고 데이터를 수집하여 Microsoft로 보낼지 여부를 제어하는 방법을 설명합니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 5d65a1333f3fc0f41bdcb5b7ac1f5284f32a03cc
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745543"
---
# <a name="enable-or-disable-usage-data-collection-for-azure-data-studio"></a>Azure Data Studio의 사용량 현황 데이터 수집 사용 또는 사용 안 함

## <a name="how-to-disable-telemetry-reporting"></a>원격 분석 보고를 사용하지 않도록 설정하는 방법

Azure Data Studio에서는 사용량 현황 데이터를 수집한 후 Microsoft로 보내 제품 및 서비스를 개선합니다. 자세히 알아보려면 [개인정보처리방침](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)을 읽어보세요.

사용량 현황 데이터를 Microsoft로 보내지 않으려는 경우 *telemetry.enableTelemetry* 설정을 *false*로 지정할 수 있습니다.

Azure Data Studio의 모든 원격 분석 이벤트를 대기하도록 하려면 **파일** > **기본 설정** > **설정**에서 다음 옵션을 추가합니다.

```json
    "telemetry.enableTelemetry": false
```

**중요한 알림**: 이 옵션을 적용하려면 Azure Data Studio를 다시 시작해야 합니다. 

## <a name="how-to-disable-crash-reporting"></a>충돌 보고를 사용하지 않도록 설정하는 방법

충돌 보고를 사용하지 않도록 설정하려면 **파일** > **기본 설정** > **설정**에서 다음 옵션을 추가합니다.

```json
    "telemetry.enableCrashReporter": false
```

**중요한 알림**: 이 옵션을 적용하려면 Azure Data Studio를 다시 시작해야 합니다.

## <a name="additional-resources"></a>추가 리소스
- [작업 영역 및 사용자 설정](settings.md)
