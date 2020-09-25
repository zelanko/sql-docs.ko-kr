---
title: 스키마 비교 확장
description: Azure Data Studio 스키마 비교 확장을 설치하여 두 개의 데이터베이스를 손쉽게 비교하고 하나의 데이터베이스가 다른 하나와 일치하도록 선택적으로 변경하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 35afe56806ad1c24b1fa6ae1f03978d7f6558af4
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123350"
---
# <a name="schema-compare-extension"></a>스키마 비교 확장

스키마 비교 확장은 두 데이터베이스 정의를 비교하고 원본에서 대상으로 차이점을 적용하는 데 사용할 수 있는 간편한 환경을 제공합니다.

## <a name="features"></a>기능

* 두 dacpac 파일 또는 데이터베이스의 스키마 비교
* 원본과 일치하도록 대상에 대해 수행해야 하는 작업 세트로 결과를 표시
* 결과에 나열된 작업을 선택적으로 제외
* 비교 범위를 제어하는 옵션 설정
* 대상에 변경 내용 적용 또는 동일한 효과를 사용하여 스크립트 생성
* 비교 저장

![스키마 비교: 예시 비교](media/schema-compare-extension/schema-compare.png)

## <a name="why-would-i-use-the-schema-compare-extension"></a>스키마 비교 확장을 사용하는 이유는 무엇인가요?

다른 데이터베이스 버전을 수동으로 관리하고 동기화하는 것은 지루할 수 있습니다. 스키마 비교 확장은 데이터베이스를 비교하는 프로세스를 간소화하고, 동기화할 때 모든 권한을 제공합니다. 특정 차이점을 선택적으로 필터링하고 변경 내용을 적용하기 전에 차이점을 범주화할 수 있습니다. 스키마 비교 확장은 시간과 코드를 절약하는 신뢰할 수 있는 도구입니다.

![스키마 비교: 옵션 대화 상자 참조](media/schema-compare-extension/schema-compare-options.png)

## <a name="install-the-extension"></a>확장 설치

1. 확장 아이콘을 선택하여 사용 가능한 확장을 표시합니다.

    ![확장 관리자 아이콘](media/add-extensions/extension-manager-icon.png)

2. **스키마 비교** 확장을 검색하고 선택하여 세부 정보를 확인합니다. **설치**를 선택하여 확장을 추가합니다.

3. 설치가 완료되면 확장을 **다시 로드하여** Azure Data Studio에서 사용하도록 설정합니다(확장을 처음 설치하는 경우에만 필요).

## <a name="launch-a-schema-compare"></a>스키마 비교 시작

1. 스키마 비교 대화 상자를 열려면 개체 탐색기에서 데이터베이스를 **마우스 오른쪽 단추로 클릭**하고 **스키마 비교**를 선택합니다. 선택한 데이터베이스는 비교 시 원본 데이터베이스로 설정됩니다.

    ![스키마 비교 시작 메뉴](media/schema-compare-extension/schema-compare-launch.png)

2. 줄임표(...) 중 하나를 선택하여 스키마 비교의 원본 및 대상을 변경하고 [확인]을 선택합니다.

    ![스키마 비교 원본/대상 선택](media/schema-compare-extension/schema-compare-select-source-target.png)

3. 비교를 사용자 지정하려면 도구 모음에서 **옵션** 단추를 선택합니다.

4. 비교 결과를 보려면 **비교**를 선택합니다.

## <a name="next-steps"></a>다음 단계

스키마 비교에 대한 자세한 내용은 [스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)를 참조하세요.
[여기](https://github.com/microsoft/azuredatastudio/issues)서 문제 및 기능 요청을 보고하세요.