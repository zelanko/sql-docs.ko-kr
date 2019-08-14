---
title: Azure Data Studio용 SandDance
titleSuffix: Azure Data Studio
description: Azure Data Studio에서 SandDance를 사용하는 방법
ms.custom: seodec18
ms.date: 07/03/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a96bde6a66642bf02cc076c3d4d4f3ac44e02a3f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959339"
---
# <a name="sanddance-for-azure-data-studio-preview"></a>Azure Data Studio SandDance(미리 보기)
이제 Azure Data Studio에서는 작업 중인 .csv 및 .tsv 파일의 시각화를 빠르게 만드는 방법을 제공합니다. 여기에는 SQL Server 2019 빅 데이터 클러스터의 HDFS에 있는 파일 또는 로컬 파일이 포함됩니다. 이 확장은 데이터를 빠르게 확인하고 진행 상황을 파악하려고 하는 경우에 유용합니다. 이를 위해 데이터 시각화를 바로 생성할 수 있는 Microsoft Research의 SandDance라는 기술을 사용합니다.

![sanddance-animation](https://user-images.githubusercontent.com/11507384/54236654-52d42800-44d1-11e9-859e-6c5d297a46d2.gif)

SandDance는 이해하기 쉬운 보기를 사용하여 데이터에 관한 인사이트를 찾아 데이터에 근거한 스토리를 전하거나, 증거에 기반한 사례를 구축하거나, 가설을 테스트하거나, 표면 설명을 심층 분석하거나, 구매 의사 결정을 지원하거나, 데이터를 더 광범위한 실제 문맥에 연결할 수 있습니다.

SandDance는 데이터베이스의 행과 화면의 표시 간에 일대일 매핑을 적용하는 단위 시각화를 사용합니다.
보기 간의 원활한 애니메이션 전환을 통해 컨텍스트를 유지하면서 데이터를 조작할 수 있습니다.

## <a name="usage"></a>사용법

[파일] 메뉴에서 [폴더 열기]를 사용하거나 [Ctrl+K Ctrl+O]를 사용하여 .CSV 파일이 포함된 디렉터리를 엽니다.  그런 다음 탐색기 패널 내에서 .csv 또는 .tsv 파일을 마우스 오른쪽 단추로 클릭하고 *View in SandDance*(SandDance에서 보기)를 선택합니다.

SQL Server 2019 빅 데이터 클러스터에 연결된 경우에 HDFS의 .csv 또는 .tsv 파일을 마우스 오른쪽 단추로 클릭하고 *View in SandDance*(SandDance에서 보기)를 선택합니다.

## <a name="known-issues"></a>알려진 문제

현재 데이터의 첫 번째 열은 고유한 식별자여야 합니다.

현재 시각화되는 행 수는 제한되지 않습니다. 그러나 행 수에 비례하여 메모리 소비가 증가하므로 데이터 세트 또는 보기를 10만 개 행으로 제한하는 것이 좋습니다.

[알려진 문제](https://microsoft.github.io/SandDance/#known-issues)를 참조하세요.

## <a name="release-notes"></a>릴리스 정보

### <a name="100"></a>1.0.0

azdata-sanddance의 초기 릴리

## <a name="next-steps"></a>Next Steps
자세히 알아보려면 [GitHub 리포지토리를 참조](https://github.com/Microsoft/SandDance)하세요.
