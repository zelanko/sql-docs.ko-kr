---
title: Azure SQL Managed Instance 확장
titleSuffix: Azure Data Studio
description: Azure Data Studio에서 Azure SQL 관리되는 인스턴스 사용
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: d443292fb091679d3d6a18d557a5a7aac464fdec
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041145"
---
# <a name="managed-instance-support-for-azure-data-studio-preview"></a>Azure Data Studio에 대한 Managed Instance 지원(미리 보기)

이 확장을 통해 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio)에서 [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index)를 사용할 수 있습니다. 이 확장은 다음과 같은 기능을 제공합니다.

- 관리되는 인스턴스(vCores, 사용된 스토리지)의 속성을 표시.
- 직전 2시간 동안 CPU 및 스토리지 사용량을 모니터링.
- 구성 경고 및 튜닝 권장 사항을 표시.
- 데이터베이스 복제본의 상태를 표시.
- 필터링된 오류 로그를 표시.

## <a name="installations"></a>설치

[Azure Data Studio 설명서](https://docs.microsoft.com/sql/azure-data-studio/extensions)의 단계에 따라 Managed Instance 확장의 공식 릴리스를 설치할 수 있습니다.
확장 창에서 "Managed Instance" 확장을 검색하여 설치합니다.  후속 확장 업데이트에 대한 알림이 자동으로 제공됩니다.

Managed Instance 확장을 설치하면 Azure Data Studio에 `Managed Instance` 탭이 표시됩니다. 이 탭에서 Managed Instance 관련 정보를 찾을 수 있습니다.

## <a name="properties"></a>속성

이 확장을 통해 Managed Instance의 기술 특성과 일부 리소스 사용량을 확인할 수 있습니다.

![관리되는 인스턴스 속성](media/azure-sql-mi-extension/ads-mi-tab1.png)

첫 번째 블레이드에서 다음과 같은 세부 정보를 볼 수 있습니다.

- **기본 속성** - 사용 가능한 vCores 수, 메모리, 스토리지, 현재 서비스 계층 및 하드웨어 생성, 인스턴스 로그 쓰기 처리량 또는 파일 IO/처리량 특성과 같은 IO 특성 등
- **로컬 SSD 저장소 사용량**. 범용 서비스 계층에서만 **TEMPDB** 파일이 로컬에 배치되는 반면, 중요 비즈니스용 계층에서는 모든 데이터베이스 파일이 로컬 SSD 저장소에 배치됩니다. 이 섹션에서는 Managed Instance에서 로컬 저장소 공간을 얼마나 사용하는지 확인할 수 있습니다.
- **Azure Premium Disk Storage 사용량** - 범용 서비스 계층의 사용자 및 시스템 데이터베이스 사용은 Azure Premium Storage에 배치됩니다. 여기에서 사용한 데이터 양과 남은 스토리지 및 파일 수를 확인할 수 있습니다. 중요 비즈니스용 서비스 계층에서는 이 섹션이 비어 있습니다.
- **리소스 사용량** - 직전 2시간 동안 인스턴스에서 사용한 스토리지 및 CPU를 표시합니다. 제한에 도달할 경우 인스턴스 크기를 늘립니다.

## <a name="recommendations"></a>권장 사항

이 확장은 Managed Instance를 최적화하는 데 도움이 될 수 있는 몇 가지 권장 사항 및 경고를 제공합니다.

![Managed Instance 권장 사항](media/azure-sql-mi-extension/ads-mi-tab2.png)

이 표에 나와 있는 권장 사항 중 일부는 다음과 같습니다.

- 스토리지 공간 제한에 도달하면 스토리지 제한에 도달하는 데이터베이스가 읽기 쿼리를 처리하지 못할 수 있으므로 불필요한 데이터를 삭제하거나 인스턴스 스토리지 크기를 늘려야 합니다.
- 인스턴스 처리량 제한에 도달하면(GP에서 ~ 22MB/s를 로드하거나 BC에서 ~ 48MB/s를 로드하는 경우) 관리되는 인스턴스는 백업을 수행할 수 있도록 로드를 제한합니다.
- 메모리 압력 - 페이지 예상 수명이 짧거나 `PAGEIOLATCH` 대기 통계가 많을 경우 이는 인스턴스가 메모리에서 페이지를 제거하고 지속적으로 디스크에서 더 많은 페이지를 로드하려 하고 있음을 나타내는 것일 수 있습니다.
- 로그 파일 제한 - 로그가 [범용 서비스 계층에 대한 파일 IO 제한](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)에 도달하는 경우 더 나은 성능을 얻으려면 파일 크기를 늘려야 할 수 있습니다.
- 데이터 파일 제한 - 데이터 파일이 [범용 서비스 계층에 대한 파일 IO 제한](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)에 도달하는 경우 더 나은 성능을 얻으려면 파일 크기를 늘려야 할 수 있습니다. 이 문제로 인해 메모리 압력이 유발되거나 백업 속도가 느려질 수 있습니다.
- 가용성 문제 - 가상 로그 파일 수가 많을 경우 성능에 영향을 미칠 수 있고, 프로세스 오류 시 범용 서비스 계층에서 데이터베이스 복구 시간이 길어질 수 있습니다.

정기적으로 이러한 권장 사항을 검토하고 근본 원인을 조사하여 정정 작업을 수행해야 합니다. 관리되는 인스턴스 확장은 보고된 문제 중 일부를 완화하기 위해 실행할 수 있는 스크립트를 제공합니다.

## <a name="replicas"></a>복제본

관리되는 인스턴스 확장을 사용하면 Managed Instance의 데이터베이스 복제본 상태를 확인할 수 있습니다.

![관리되는 인스턴스 복제본](media/azure-sql-mi-extension/ads-mi-tab3.png)

범용 서비스 계층에서 모든 데이터베이스에는 단일 (주) 복제본이 있으며, 중요 비즈니스용 인스턴스에는 모든 데이터베이스에 하나의 주 복제본과 3개의 보조 복제본(하나는 읽기 전용 워크로드에 사용됨)이 있습니다. 여기에서 동기화 프로세스를 모니터링하고 모든 보조 복제본이 주 복제본과 동기화되었는지 확인할 수 있습니다.

## <a name="logs"></a>로그

관리되는 인스턴스 확장에는 가장 관련성이 높은 최근 SQL 오류 로그 항목이 표시됩니다.

![관리되는 인스턴스 로그 항목](media/azure-sql-mi-extension/ads-mi-tab4.png)

Managed Instance는 수많은 로그 항목을 내보내는데, 대부분은 내부/시스템 정보입니다. 일부 로그 항목은 논리적 데이터베이스 이름 대신 실제 데이터베이스 이름(`GUID` 값)을 표시합니다.

Managed Instance 확장은[Dimitri Furman 방법](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506)을 기반으로 불필요한 로그 항목을 필터링하고 실제 이름 대신 논리적 파일 이름을 표시합니다.

## <a name="reporting-problems"></a>문제 보고

관리되는 인스턴스 확장에 문제가 발생하는 경우 [Extension GitHub 프로젝트](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues)에 문제를 보고합니다.

## <a name="maintainers"></a>유지 관리자

- [Jovan Popovic(MSFT)](https://github.com/jovanpop_msft) - [@jovanpop_msft](https://twitter.com/JovanPop_MSFT)

## <a name="code-of-conduct"></a>사용 규정

이 프로젝트는 [Microsoft 오픈 소스 준수 사항][conduct-code]을 채택했습니다.
자세한 내용은 [준수 사항 FAQ][conduct-FAQ]를 참조하고, 추가 질문이나 의견이 있는 경우에는 [opencode@microsoft.com ][conduct-email]으로 문의하세요.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
