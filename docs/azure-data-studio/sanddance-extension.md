---
title: Azure Data Studio에 대 한 sandDance
titleSuffix: Azure Data Studio
description: Azure Data Studio SandDance 사용 하는 방법
ms.custom: seodec18
ms.date: 07/03/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 466b2b60548d1dcef104979d1e291d44bf53b3de
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67563986"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>Azure Data Studio (미리 보기)에 대 한 sandDance
Azure Data Studio에는 이제에서 작업 하는.csv 및.tsv 파일에 대 한 빠른 시각화를 만드는 방법을 제공 합니다. SQL Server 2019 빅 데이터 클러스터에 로컬 파일 또는 파일 HDFS에 포함 됩니다. 이 확장 빠른 데이터를 확인 하 고 진행 상황을 이해 하도록 하려는 경우 유용 합니다. 데이터의 전체 시각화를 생성할 수 있는 Microsoft Research에서 SandDance 라는 기술을 사용 합니다.

![sanddance 애니메이션](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

이해 하기 쉬운 뷰, 데이터를 지 원하는 스토리를 알리는 설정 도움말의 증명 정보에 따라 사례를 구축, 하는 데이터에 대 한 통찰력 SandDance에서는 사용 하 여 가설을 테스트, 화면 설명에 자세히, 구매에 대 한 의사 결정 지원 또는 더 광범위 한, 실제 컨텍스트에 데이터를 연결 합니다.

SandDance 화면에서 데이터베이스의 행과 표시 간에 일대일 매핑이 적용 되는 단위 시각화를 사용 합니다.
부드러운 애니메이션된 전환을 보기에는 데이터와 상호 작용할 때 컨텍스트를 유지 관리할 수 있습니다.

## <a name="usage"></a>사용법

폴더 열기 또는 [Ctrl + K Ctrl + O]를 포함 하는 디렉터리를 열고 사용 파일 메뉴에서 시작 합니다. CSV 파일입니다.  다음으로에서 탐색기 패널 내에서.csv 또는.tsv 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 *SandDance 보기*합니다.

SQL Server 2019 빅 데이터 클러스터에 연결 되 고 선택 하는 경우 HDFS의.csv 또는.tsv 파일을 마우스 오른쪽 단추로 클릭 *SandDance 보기*합니다.

## <a name="known-issues"></a>알려진 문제

현재 데이터 고유 식별자로 첫 번째 열에 있어야 합니다.

현재 시각화 되는 행 수를 제한 하지 않습니다. 그러나 메모리 소비가 비례적으로 행의 수 있으므로 데이터 집합 또는 뷰를 약 100 개 행으로 제한 된다는 것이 좋습니다.

참조 [알려진 문제](https://microsoft.github.io/SandDance/#known-issues)

## <a name="release-notes"></a>릴리스 정보

### <a name="100"></a>1.0.0

Azdata sanddance의 초기 릴리스

## <a name="next-steps"></a>다음 단계
자세한 내용은 [GitHub 리포지토리를 방문 합니다.](https://github.com/Microsoft/SandDance)
