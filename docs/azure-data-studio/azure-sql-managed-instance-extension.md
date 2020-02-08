---
title: Azure SQL Database 관리되는 인스턴스 확장
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
ms.openlocfilehash: 2269c594bd0fff036d4fe5d5d722aa5d78d4ca6d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75883992"
---
# <a name="azure-sql-database-managed-instance-dashboard-for-azure-data-studio-preview"></a>Azure Data Studio용 Azure SQL Database 관리되는 인스턴스 대시보드(미리 보기)

Azure SQL Database 관리되는 인스턴스 확장은 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio)에서 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index)를 사용하기 위한 대시보드를 제공합니다. 이 확장은 다음과 같은 기능을 제공합니다.

- vCore 및 사용된 스토리지를 포함하여 관리되는 인스턴스 속성을 표시
- 이전 2시간 동안 CPU 및 스토리지 사용량을 모니터링
- 구성 경고 및 튜닝 권장 사항을 표시
- 데이터베이스 복제본의 상태를 표시
- 필터링된 오류 로그를 표시

## <a name="install"></a>설치

이 확장의 공식 릴리스를 설치할 수 있습니다. [Azure Data Studio 설명서](https://docs.microsoft.com/sql/azure-data-studio/extensions)의 단계를 수행합니다.
**확장** 창에서 “관리되는 인스턴스”를 검색하여 설치합니다. 이 확장을 설치하면 후속 확장 업데이트에 대한 알림이 자동으로 제공됩니다.

그리고 Azure Data Studio에 **관리되는 인스턴스** 탭이 표시됩니다. 이 탭에서 관리되는 인스턴스 관련 정보를 찾을 수 있습니다.

## <a name="properties"></a>속성

확장은 관리되는 인스턴스의 기술 특성 및 일부 리소스 사용을 표시합니다.

[ ![관리되는 인스턴스 속성](media/azure-sql-mi-extension/ads-mi-tab1.png )](media/azure-sql-mi-extension/ads-mi-tab1.png#lightbox)

위쪽 창에는 다음과 같은 세부 정보가 표시됩니다.

- **속성** 사용 가능한 vCore, 메모리 및 스토리지를 포함하여 관리되는 인스턴스에 대한 기본 정보를 가져옵니다. 또한 현재 서비스 계층, 하드웨어 생성 및 IO 특성(예: 인스턴스 로그 쓰기 처리량 또는 파일 I/O 처리량 특성)도 찾을 수 있습니다.
- **로컬 SSD 저장소** 범용 서비스 계층에서 **TempDB** 파일은 로컬에 저장됩니다. 중요 비즈니스용 서비스 계층에서는 _모든_ 데이터베이스 파일이 로컬 SSD 저장소에 배치됩니다. 이 섹션에서는 관리되는 인스턴스에서 로컬 스토리지 공간을 얼마나 사용하는지 확인할 수 있습니다.
- **Azure Premium Disk Storage**. 범용 서비스 계층을 사용하는 경우 사용자 및 시스템 데이터베이스 파일은 모두 Azure Premium 스토리지에 배치됩니다. 이 섹션에서는 사용된 데이터의 양, 파일 수 및 사용 가능한 스토리지를 확인할 수 있습니다. 중요 비즈니스용 서비스 계층에서는 이 섹션이 비어 있습니다.
- **리소스 사용량** 이전 2시간 동안 관리되는 인스턴스가 사용한 스토리지 및 CPU의 비율을 확인합니다. 이를 통해 인스턴스가 한도에 근접하는 경우 인스턴스 크기를 늘릴 수 있습니다.

## <a name="recommendations"></a>권장 사항

**관리되는 인스턴스** 탭에서 두 번째 창을 선택하면 관리되는 인스턴스를 최적화하는 데 도움이 되는 권장 사항 및 경고가 표시됩니다.

[ ![관리되는 인스턴스 권장 사항](media/azure-sql-mi-extension/ads-mi-tab2.png )](media/azure-sql-mi-extension/ads-mi-tab2.png#lightbox)

다음과 같은 권장 사항이 표시될 수 있습니다.

- **저장소 공간 제한에 도달**. 불필요한 데이터를 삭제하거나 인스턴스 스토리지 크기를 늘리세요. 스토리지 제한에 도달한 데이터베이스는 읽기 쿼리도 처리하지 못할 수 있습니다.
- **인스턴스 처리량 제한에 도달**. 서비스 계층의 제한에 근접하여 로드하는 경우 사용자에게 알립니다. 범용의 경우 22MB/s, 중요 비즈니스용의 경우 48MB/s입니다. 관리되는 인스턴스는 백업을 수행할 수 있도록 부하를 제한한다는 점을 유의하세요.
- **메모리 압력**. 페이지 예상 수명이 짧거나 `PAGEIOLATCH` 대기 통계가 많을 경우 이는 인스턴스가 메모리에서 페이지를 제거하고 지속적으로 디스크에서 더 많은 페이지를 로드하려 하고 있음을 나타내는 것일 수 있습니다.
- **로그 파일 제한**. 로그 파일이 [범용 서비스 계층에 대한 파일 I/O 제한](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)에 근접하는 경우 더 나은 성능을 얻으려면 로그 파일 크기를 늘려야 할 수 있습니다.
- **데이터 파일 제한**. 데이터 파일이 [범용 서비스 계층에 대한 파일 I/O 제한](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)에 근접하는 경우 더 나은 성능을 얻으려면 데이터 파일 크기를 늘려야 할 수 있습니다. 이 문제로 인해 메모리 압력이 유발되거나 백업 속도가 느려질 수 있습니다.
- **가용성 문제**. 가상 로그 파일 수가 많으면 성능에 영향을 줄 수 있습니다. 프로세스 오류가 발생하면 이러한 문제로 인해 범용 서비스 계층에서 데이터베이스 복구가 길어질 수 있습니다.

정기적으로 이러한 권장 사항을 검토하고 근본 원인을 조사하여 문제를 해결하기 위한 조치를 취해야 합니다. Azure SQL Database 관리되는 인스턴스 확장은 보고된 문제 중 일부를 완화하기 위해 실행할 수 있는 스크립트를 제공합니다.

## <a name="replicas"></a>복제본

**관리되는 인스턴스** 탭의 세 번째 창에서는 관리되는 인스턴스의 데이터베이스 복제본 상태를 보여 줍니다.

[ ![관리되는 인스턴스 복제본](media/azure-sql-mi-extension/ads-mi-tab3.png )](media/azure-sql-mi-extension/ads-mi-tab3.png#lightbox)

범용 서비스 계층에서 모든 데이터베이스에는 단일 (기본) 복제본이 있습니다. 중요 비즈니스용 계층 인스턴스에서 모든 데이터베이스에는 기본 복제본 1개와 보조 복제본 3개가 있으며, 이 중 하나는 읽기 전용 작업에 사용됩니다. **복제본** 창에서 동기화 프로세스를 모니터링하고 모든 보조 복제본이 주 복제본과 동기화되었는지 확인할 수 있습니다.

## <a name="logs"></a>로그

**관리되는 인스턴스**의 네 번째 창에는 최신 및 관련 SQL 오류 로그 항목이 표시됩니다.

[ ![관리되는 인스턴스 로그 항목](media/azure-sql-mi-extension/ads-mi-tab4.png )](media/azure-sql-mi-extension/ads-mi-tab4.png#lightbox)

관리되는 인스턴스는 수많은 로그 항목을 생성하지만, 대부분은 내부/시스템 정보입니다. 또한 일부 로그 항목은 논리적 데이터베이스 이름 대신 실제 데이터베이스 이름(`GUID` 값)을 표시합니다.

Azure SQL Database 관리되는 인스턴스 확장은 [Dimitri Furman 방법](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506)에 따라 불필요한 로그 항목을 필터링합니다. 또한 확장은 실제 이름 대신 실제 논리적 파일 이름을 표시합니다.

## <a name="reporting-problems"></a>문제 보고

Azure SQL Database 관리되는 인스턴스 확장에 문제가 발생하는 경우 [확장 GitHub 프로젝트](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues)로 이동하여 문제를 보고합니다.

## <a name="code-of-conduct"></a>사용 규정

이 프로젝트는 [Microsoft 오픈 소스 준수 사항][conduct-code]을 채택했습니다.

자세한 내용은 [준수 사항 FAQ][conduct-FAQ]를 참조하고, 추가 질문이나 의견이 있는 경우에는 [opencode@microsoft.com][conduct-email]으로 문의하세요.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [GitHub 프로젝트](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/)를 참조하세요.

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
