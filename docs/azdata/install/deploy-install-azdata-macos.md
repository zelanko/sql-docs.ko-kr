---
title: macOS용 Azure Data CLI(azdata) 설치
titleSuffix: ''
description: macOS에 Azure Data CLI(azdata) 도구를 설치하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0e3d7217ef917c794f1c497f7c5548588c2da1ba
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257383"
---
# <a name="install-azure-data-cli-azdata-on-macos"></a>macOS에 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] 설치

macOS 플랫폼의 경우, Homebrew 패키지 관리자를 사용하여 `azdata-cli`를 설치할 수 있습니다. CLI 패키지는 다음과 같은 macOS 버전에서 테스트되었습니다.

- 10.13 High Sierra
- 10.14 Mojave
- 10.15 Catalina

## <a name="install-with-homebrew"></a>Homebrew로 설치

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>`azdata-cli`는 Homebrew `python3`, `freetds`, `unixodbc`, `zeromq` 패키지에 종속되어 있으므로 이들 패키지를 설치합니다. `azdata-cli`는 Homebrew에 게시된 이들 종속성의 최신 버전과 호환이 가능하도록 보장됩니다.

## <a name="verify-install"></a>설치 확인

```bash
azdata
azdata --version
```

## <a name="update"></a>업데이트

로컬 리포지토리 정보를 업데이트한 후 `azdata-cli` 패키지를 업그레이드해야 합니다.

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>제거

Homebrew를 사용하여 `azdata-cli` 패키지를 제거합니다.

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.

[Azure Arc 지원 데이터 서비스](/azure/azure-arc/data/)와 함께 azdata 사용
