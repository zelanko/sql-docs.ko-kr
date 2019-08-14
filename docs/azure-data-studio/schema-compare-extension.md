---
title: 스키마 비교 확장
titleSuffix: Azure Data Studio
description: Azure Data Studio용 스키마 비교 확장(미리 보기) 설치 및 사용
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a51d64202d3d906b3106092084628b0a961297ea
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959323"
---
# <a name="schema-compare-extension-preview"></a>스키마 비교 확장(미리 보기)
스키마 비교 확장은 .dacpac 파일 및 데이터베이스를 비교하고 원본에서 대상으로 변경 내용을 적용하는 데 사용할 수 있는 간편한 환경을 제공합니다.

이 환경은 현재 최초 미리 보기로 제공됩니다. [여기](https://github.com/microsoft/azuredatastudio/issues)서 문제 및 기능 요청을 보고하세요.

## <a name="install-the-schema-compare-extension"></a>스키마 비교 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택합니다.
2. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.
1. 원하는 확장(스키마 비교)을 선택하고 **설치**합니다.

## <a name="how-do-i-start-a-schema-comparison"></a>스키마 비교를 어떻게 시작하나요?
* 스키마 비교의 기본 진입점은 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **스키마 비교**를 클릭하는 것입니다.
* 사용자는 **스키마 비교**를 검색하여 명령 팔레트(Ctrl + Shift + P)에서 스키마 비교 대화 상자를 시작할 수도 있습니다.

## <a name="why-would-i-use-the-schema-compare"></a>스키마 비교를 사용하는 이유는 무엇인가요?
스키마 비교는 .dacpac 파일과 데이터베이스의 스키마를 비교하고 변경 내용을 적용하는 기능을 추가하기 위해 만들어졌습니다.

## <a name="next-steps"></a>다음 단계
스키마 비교에 대해 자세히 알아보려면 [설명서를 참조하세요.](https://docs.microsoft.com/sql/ssdt/how-to-use-schema-compare-to-compare-different-database-definitions)


