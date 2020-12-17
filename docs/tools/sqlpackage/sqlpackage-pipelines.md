---
title: 개발 파이프라인의 SqlPackage
description: 설치된 빌드 번호를 확인하여 SqlPackage.exe의 데이터베이스 개발 파이프라인 문제를 해결하는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 11/4/2020
ms.openlocfilehash: 002d145328ca101fee467428e5b7c8b0ff1fdd95
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97577928"
---
# <a name="sqlpackage-in-development-pipelines"></a>개발 파이프라인의 SqlPackage

**SqlPackage.exe** 는 여러 데이터베이스 개발 작업을 자동화하고 CI/CD 파이프라인에 통합할 수 있는 명령줄 유틸리티입니다.

## <a name="managed-virtual-environments"></a>관리되는 가상 환경

GitHub Actions가 호스트하는 실행기와 Azure Pipelines VM 이미지에 사용되는 가상 환경은 [virtual-environments](https://github.com/actions/virtual-environments) GitHub 리포지토리에서 관리됩니다.  SqlPackage는 `windows-latest` 환경에 포함되어 있으며, 각 SqlPackage 릴리스의 몇 주 이내에 이미지 업데이트가 수행됩니다.

## <a name="checking-the-sqlpackage-version"></a>SqlPackage 버전 확인

문제 해결 활동 시 사용 중인 SqlPackage 버전을 알아야 합니다.  `/version` 매개 변수로 SqlPackage를 실행하는 단계를 파이프라인에 추가하면 이 정보를 캡처할 수 있습니다.  예제는 Microsoft 및 GitHub 관리 환경에 따라 아래에 제공되며, 자체 호스팅 환경에서는 작업 디렉터리의 설치 경로가 다를 수 있습니다.

### <a name="azure-pipelines"></a>Azure Pipelines

Azure Pipeline에서 [script](https://docs.microsoft.com/azure/devops/pipelines/yaml-schema#script) 키워드를 활용하면 SqlPackage 버전 번호를 출력하는 단계를 Azure Pipeline에 추가할 수 있습니다.

```yaml
- script: sqlpackage.exe /version
  workingDirectory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  displayName: 'get sqlpackage version'
```

### <a name="github-actions"></a>GitHub 작업

GitHub 작업 워크플로에서 [run](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions) 키워드를 활용하면 SqlPackage 버전 번호를 출력하는 단계를 GitHub 작업에 추가할 수 있습니다.

```yaml
- name: get sqlpackage version
  working-directory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  run: ./sqlpackage.exe /version
```

:::image type="content" source="media/sqlpackage-pipelines-github-action.png" alt-text="빌드 번호 15.0.4897.1을 표시하는 GitHub 작업 출력":::

## <a name="next-steps"></a>다음 단계

- [sqlpackage](sqlpackage.md)에 대한 자세한 정보
