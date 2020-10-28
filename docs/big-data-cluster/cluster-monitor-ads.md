---
title: Azure Data Studio를 사용하여 클러스터 모니터링
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 Azure Data Studio를 사용하여 클러스터를 모니터링합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4c4dc9956b8c3f9802feb839096195c09664d0d6
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378468"
---
# <a name="monitor-cluster-status-with-azure-data-studio"></a>Azure Data Studio를 사용하여 클러스터 상태 모니터링

이 문서에서는 Azure Data Studio를 사용하여 빅 데이터 클러스터의 상태를 보는 방법을 설명합니다.

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> Azure Data Studio 사용

[Azure Data Studio](https://aka.ms/getazuredatastudio)의 최신 **참가자 빌드** 를 다운로드한 후에 SQL Server 빅 데이터 클러스터 대시보드를 사용하여 서비스 엔드포인트와 빅 데이터 클러스터 상태를 볼 수 있습니다. 아래 기능 중 일부는 Azure Data Studio 참가자 빌드에서만 처음으로 제공되는 것입니다.

1. 먼저 Azure Data Studio에서 빅 데이터 클러스터에 연결합니다. 자세한 내용은 [Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

1. 빅 데이터 클러스터 엔드포인트를 마우스 오른쪽 단추로 클릭하고 **관리** 를 클릭합니다.

   ![관리를 마우스 오른쪽 단추로 클릭](media/view-cluster-status/right-click-manage.png)

1. **SQL Server 빅 데이터 클러스터** 탭을 선택하여 빅 데이터 클러스터 대시보드에 액세스합니다.

   ![빅 데이터 클러스터 대시보드](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>서비스 엔드포인트

빅 데이터 클러스터의 다양한 서비스에 쉽게 액세스할 수 있어야 합니다. 빅 데이터 클러스터 대시보드는 서비스 엔드포인트를 확인하고 복사할 수 있는 서비스 엔드포인트 테이블을 제공합니다.

![서비스 엔드포인트](media/view-cluster-status/service-endpoints.png)

서비스에는 해당 서비스에 연결하기 위한 엔드포인트가 필요할 때 복사하여 붙여넣을 수 있는 엔드포인트가 표시됩니다. 예를 들어 엔드포인트 오른쪽에 있는 복사 아이콘을 클릭한 다음, 해당 엔드포인트를 요청하는 텍스트 창에 붙여넣을 수 있습니다. 클러스터 관리 서비스 엔드포인트는 [클러스터 상태 Notebook](#notebook)을 실행하는 데 필요합니다.

### <a name="dashboards"></a>대시보드

서비스 엔드포인트 테이블은 모니터링에 사용되는 몇 개의 대시보드도 공개합니다.

- 메트릭(Grafana)
- 로그(Kibana)
- Spark 작업 모니터링
- Spark 리소스 관리

이러한 링크를 직접 클릭할 수 있습니다. 대시보드에 액세스하려면 인증해야 합니다. 메트릭 대시보드와 로그 대시보드의 경우, 환경 변수 **AZDATA_USERNAME** 및 **AZDATA_PASSWORD** 를 사용하여 배포 시점에 설정한 컨트롤러 관리자 자격 증명을 제공하세요. Spark 대시보드는 게이트웨이(Knox) 자격 증명을 사용합니다. 즉, AD에 통합된 클러스터의 AD ID이거나 클러스터에서 기본 인증을 사용하고 있다면 **AZDATA_USERNAME** 과 **AZDATA_PASSWORD** 입니다.

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

### <a name="cluster-status-notebook"></a><a id="notebook"></a> 클러스터 상태 Notebook

1. 클러스터 상태 Notebook을 시작하여 빅 데이터 클러스터의 클러스터 상태를 볼 수도 있습니다. Notebook을 시작하려면 **클러스터 상태** 작업을 클릭합니다.

    ![시작](media/view-cluster-status/cluster-status-launch.png)

2. 시작하기 전에 다음 항목이 필요합니다.

    - 빅 데이터 클러스터 이름
    - 컨트롤러 사용자 이름
    - 컨트롤러 암호
    - 컨트롤러 엔드포인트

    빅 데이터 클러스터의 기본 이름은 배포 중에 사용자 지정하지 않은 경우 **mssql-cluster** 입니다. 서비스 엔드포인트 테이블의 빅 데이터 클러스터 대시보드에서 컨트롤러 엔드포인트를 찾을 수 있습니다. 엔드포인트는 **클러스터 관리 서비스** 로 나열됩니다. 자격 증명을 모르는 경우 클러스터를 배포한 관리자에게 문의합니다.

3. 위쪽 도구 모음에서 **셀 실행** 을 클릭합니다.

4. 프롬프트를 따라 자격 증명을 제공합니다. 빅 데이터 클러스터 이름, 컨트롤러 사용자 이름 및 컨트롤러 암호의 자격 증명을 각각 입력한 후에 Enter 키를 누릅니다.

    > [!Note]
    > 빅 데이터로 설정된 구성 파일이 없으면 컨트롤러 엔드포인트를 묻는 메시지가 표시됩니다. 입력하거나 붙여넣은 다음 Enter 키를 눌러 계속 진행합니다.

5. 성공적으로 연결된 경우 Notebook의 나머지 부분에 빅 데이터 클러스터의 각 구성 요소에 대한 출력이 표시됩니다. 특정 코드 셀을 다시 실행하려면 코드 셀을 마우스로 가리키고 **실행** 아이콘을 클릭합니다.


## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
