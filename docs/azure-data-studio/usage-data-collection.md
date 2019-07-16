---
title: 사용 또는 사용 현황 데이터 수집 및 크래시 보고를 사용 하지 않도록 설정
titleSuffix: Azure Data Studio
description: 이 문서에서는 사용량 및 크래시 보고 데이터는 수집 되 고 Microsoft로 전송 하는 경우를 제어 하는 방법을 설명 합니다.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 71ed86e9ad076a41099eaf4e56fe67a25b5f2c21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958943"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>에 대 한 사용 데이터 컬렉션 설정 또는 해제 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>원격 분석 보고를 사용 하지 않도록 설정 하는 방법

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 사용 현황 데이터를 수집 하 고 제품과 서비스를 개선 하기 위해 Microsoft로 보냅니다. 자세한 내용은 참조는 [개인정보취급방침](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)합니다.

Microsoft 사용 현황 데이터 보내기 않으려면 경우 설정할 수 있습니다 합니다 *telemetry.enableTelemetry* 설정을 *false*합니다.

모든 원격 분석 이벤트를 억제 [!INCLUDE[name-sos](../includes/name-sos-short.md)]에서 **파일** > **기본 설정** > **설정**, 다음 옵션을 추가 합니다.

```json
    "telemetry.enableTelemetry": false
```

**중요 알림**: 이 옵션의 다시 시작이 필요한 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 적용 합니다. 

## <a name="how-to-disable-crash-reporting"></a>작동 중단 보고를 사용 하지 않도록 설정 하는 방법

충돌 보고를 사용 하지 않도록 설정에서 **파일** > **기본 설정** > **설정**, 다음 옵션을 추가 합니다.

```json
    "telemetry.enableCrashReporter": false
```

**중요 알림**: 이 옵션의 다시 시작이 필요한 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 적용 합니다.

## <a name="additional-resources"></a>추가 자료
- [작업 영역 및 사용자 설정](settings.md)
