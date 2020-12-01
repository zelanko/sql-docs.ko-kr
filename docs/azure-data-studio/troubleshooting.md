---
title: Azure Data Studio 문제 해결
description: 로그를 가져오고 Azure Data Studio 문제를 해결하는 방법을 알아봅니다. 이 방법은 버그 보고서를 보고하는 데 유용합니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: hanqin, maghan
ms.custom: seodec18
ms.date: 11/24/2020
ms.openlocfilehash: 1d2483532589cd840f1120cfb0ac3273b41e0bb5
ms.sourcegitcommit: 2e7154475ba1f31d1aeebc8f48ac05846f793736
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "95920217"
---
# <a name="azure-data-studio-troubleshooting"></a>Azure Data Studio 문제 해결
Azure Data Studio는 `azuredatastudio` 저장소의 [GitHub 저장소 문제 추적기](https://github.com/Microsoft/azuredatastudio/issues)를 사용하여 문제 및 기능 요청을 추적합니다. 

## <a name="if-youve-experienced-any-issue"></a>문제가 발생한 경우

[GitHub 문제 추적기](https://github.com/Microsoft/azuredatastudio/issues)에 문제를 신고하고 오류 재현에 도움이 되는 세부 정보를 알려주세요. 로그 파일의 [로그 정보](#how-to-set-the-logging-level)를 포함합니다.

## <a name="writing-good-bug-reports-and-feature-requests"></a>좋은 버그 보고서 및 기능 요청 작성

문제 및 기능 요청별로 단일 문제를 제출합니다.

* 동일한 문제에 여러 버그 또는 기능 요청을 열거하지 마세요.
* 동일한 의견에 해당하지 않는 한 이슈를 댓글로 기존 이슈에 추가하지 마세요. 많은 문제가 비슷해 보이지만 원인이 다릅니다.

더 많은 정보를 제공할수록 누군가 문제를 성공적으로 재현하고 해결책을 찾을 가능성이 높아집니다. 

각 문제에 다음 정보를 포함하세요.

* Azure Data Studio 버전
* 재현 가능한 단계(1 ... 2... 3 ...) 및 예상 한 것과 실제로 본 것. 
* 이미지, 애니메이션 또는 비디오 링크. 이미지와 애니메이션은 재현 단계를 설명하지만 대체하지 ‘않습니다’.
* 문제를 보여주는 코드 조각 또는 코드 리포지토리에 대한 링크는 문제를 재현하기 위해 컴퓨터로 쉽게 끌어올 수 있습니다. 

> [!NOTE]
>  코드 조각을 복사하여 붙여넣어야 하므로 코드 조각을 미디어 파일(예: .gif)로 포함하는 것만으로는 충분하지 않습니다. 

* 개발자 도구 콘솔의 오류(도움말 | 개발자 도구 전환)

다음을 수행하세요.

* 문제 저장소를 검색하여 중복된 항목이 있는지 확인하세요. 
* 이슈에 관한 코드를 단순화하여 Microsoft에서 문제를 더욱 효과적으로 파악하도록 돕습니다. 

문제를 재현할 수 없고 더 많은 정보를 요청해도 기분 나빠하지 마세요!

## <a name="how-to-set-the-logging-level"></a>로깅 수준을 설정하는 방법

### <a name="azure-data-studio"></a>Azure Data Studio
`Developer: Set Log Level...` 명령을 실행하여 현재 세션에 대한 로그 수준을 선택합니다. 이 값은 여러 세션에서 유지되지 않으므로 Azure Data Studio를 다시 시작하면 기본 `Info` 수준으로 되돌아갑니다. 

시작 시 디버그 로깅을 사용하려면 로그 레벨을 `Debug`로 설정하고 `Developer: Reload Window` 명령을 실행하세요.

### <a name="mssql-built-in-extension"></a>MSSQL(기본 제공 확장)

`Mssql: Log Debug Info` 사용자 설정이 true로 설정된 경우 디버그 로그 정보가 `MSSQL` 출력 채널로 전송됩니다.

`Mssql: Tracing Level` 사용자 설정은 로깅의 자세한 정도를 제어하는 데 사용됩니다.

## <a name="debug-log-location"></a>디버그 로그 위치
Azure Data Studio에서 `Developer: Open Logs Folder` 명령을 실행하여 로그 경로를 엽니다. 여기에 기록하는 다양한 유형의 로그 파일이 있으며 일반적으로 사용되는 몇 가지 유형은 다음과 같습니다.

1. `renderer#.log`(예: renderer1.log) - 이 파일은 기본 프로세스에 대한 로그 파일입니다.
1. `telemetry.log` - 로그 수준이 `Trace`로 설정되면 이 파일에는 Azure Data Studio에서 보낸 원격 분석 이벤트가 포함됩니다.
1. `exthost#/exthost.log` - 확장 호스트 프로세스에 대한 로그 파일(이는 프로세스 자체일 뿐 내부에서 실행 중인 확장이 아님)
1. `exthost#/Microsoft.mssql` - MSSQL 관련 기능에 대한 핵심 논리가 많이 포함된 mssql 확장에 대한 로그
   * sqltools.log는 SQL 도구 서비스에 대한 로그입니다.
1. `exthost#/output_logging_#######` - 이러한 폴더에는 Azure Data Studio의 `Output` 패널에 표시되는 메시지가 포함됩니다. 각 파일의 이름은 `#-<Channel Name>`이므로 예를 들어 `Notebooks` 출력 채널은 `3-Notebooks.log`라는 파일로 출력 될 수 있습니다.

로그를 제공하라는 메시지가 표시되면 전체 폴더를 압축하여 올바른 로그가 포함되었는지 확인하세요. 

## <a name="next-steps"></a>다음 단계
- [문제 보고](https://github.com/Microsoft/azuredatastudio/issues)
- [Azure Data Studio란?](what-is-azure-data-studio.md)