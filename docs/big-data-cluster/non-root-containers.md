---
title: 루트가 아닌 빅 데이터 클러스터 컨테이너
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 빅 데이터 클러스터에 루트가 아닌 컨테이너를 배포하는 방법을 설명합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6371d142609b095eb6d30fcdac63cb051db22c4f
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85218182"
---
# <a name="non-root-big-data-clusters-containers"></a>루트가 아닌 빅 데이터 클러스터 컨테이너

SQL Server 2019 CU5에는 루트가 아닌 컨테이너 관련 지원이 도입되었습니다. 지원되는 모든 플랫폼에서 BDC 내에서 실행되는 모든 컨테이너 애플리케이션이 기본적으로 루트가 아닌 사용자로 시작되도록 하여, 더 안전하게 플랫폼을 구현할 수 있습니다. SQL Server 2019 CU5 해당 이미지 태그를 사용하여 모든 새 배포에 이러한 기능을 사용할 수 있습니다. 기존의 CU5 이전 BDC 배포는 이 변경의 영향을 받지 않으며 해당 클러스터의 애플리케이션은 계속 루트 사용자로 실행됩니다. 

## <a name="technical-background"></a>기술적 배경

루트가 아닌 사용자를 사용한 배포를 수용하기 위한 보안 디자인의 세부 정보를 설명하는 [이 기술 백서](https://aka.ms/sql-bdc-openshift-security)를 검토하세요. 백서에서는 빅 데이터 클러스터가 특정 사례에서 일시적으로 권한을 상승시키는 이유 및 상승되는 권한을 강조합니다. 백서 내용은 SQL Server와 Red Hat의 보안 전문가와 협업을 통해 개발되었으며 OpenShift의 보안 컨텍스트 및 기능에 중점을 두지만, BDC 보안 개념 및 디자인은 지원되는 모든 플랫폼에 적용됩니다.

> [!NOTE]
> CU5 릴리스 시점에 [앱 배포](concept-application-deployment.md) 인터페이스를 사용하여 배포되는 애플리케이션의 설치 단계는 여전히 ‘루트’ 사용자로 실행됩니다. 이 동작은 설치 도중에 애플리케이션에서 사용할 추가 패키지가 설치되기 때문에 필요합니다. 애플리케이션의 일부로 배포된 다른 사용자 코드는 권한이 낮은 사용자로 실행됩니다. 

> [!NOTE]
> 루트가 아닌 기본 설정으로 클러스터를 실행하는 것이 좋습니다. CU5 이전 동작으로 되돌리려는 경우 BDC 내의 컨테이너를 `root` 사용자로 실행하려면 새 기능 스위치 `allowRunAsRoot`를 사용하여 기본 동작을 해제할 수 있습니다. 배포 시에만 이렇게 설정할 수 있습니다. 설정하려면 `control.json` 배포 구성 파일의 `security` 섹션 아래에 있는 설정을 지정합니다.

```json
 "security": {
  …
    "allowRunAsRoot": true,
  …
}
```

> [!IMPORTANT]
> OpenShift 환경에서는 이 설정을 변경하는 것이 지원되지 않습니다.

루트가 아닌 사용자로 실행되는 BDC 내의 서비스의 결과로, 게이트웨이 엔드포인트를 통해 서비스에 연결하는 데 사용되는 자격 증명은 `root` 사용자 이름을 사용하지 않습니다. 게이트웨이 엔드포인트에 연결하는 데 사용된 애플리케이션에서 잘못된 자격 증명을 사용하는 경우 인증 오류가 표시됩니다. 게이트웨이 엔드포인트의 새 사용자 이름은 `AZDATA_USERNAME` 환경 변수를 통해 전달되는 값을 기반으로 합니다. 이때 사용자 이름은 컨트롤러 및 SQL Server 엔드포인트에 사용되는 것과 동일합니다. 이런 동작은 새 배포에만 영향을 미치며, 이전 릴리스를 사용하여 배포된 기존 빅 데이터 클러스터는 계속 `root`를 사용합니다. Active Directory 인증을 사용하도록 클러스터를 배포하는 경우 자격 증명에는 영향이 없습니다. 

## <a name="use-the-latest-azure-data-studio"></a>최신 Azure Data Studio 사용

Azure Data Studio는 게이트웨이를 통한 연결에 대해 자격 증명 변경을 투명하게 처리하여 개체 탐색기에서 HDFS 검색 환경을 사용하거나 Notebook을 통해 Spark 작업을 제출할 수 있도록 설정합니다. [최신 Azure Data Studio 참가자 빌드](../azure-data-studio/download-azure-data-studio.md#download-insiders-build-of-azure-data-studio)를 설치합니다. 이 빌드에는 이 사용 사례에 필요한 변경 내용이 포함되어 있습니다.

게이트웨이를 통해 서비스에 액세스하기 위해 자격 증명을 제공해야 하는 다른 시나리오(예: `azdata`를 사용하여 로그인, Spark의 웹 대시보드에 액세스)의 경우 올바른 자격 증명이 사용되는지 확인합니다. CU5 이전에 배포된 기존 클러스터를 대상으로 하는 경우 클러스터를 CU5로 업그레이드한 후에도 계속 `root` 사용자 이름을 사용하여 게이트웨이에 연결합니다. CU5 빌드를 사용하여 새 클러스터를 배포하는 경우 `AZDATA_USERNAME` 환경 변수에 해당하는 사용자 이름을 제공하여 로그인합니다.

## <a name="configuration-file-switches"></a>구성 파일 스위치

CU5부터 Pod 및 노드 메트릭의 수집을 제어하는 두 가지 기능 스위치가 새로 추가되었습니다. Kubernetes 인프라를 모니터링하기 위해 다른 솔루션을 사용하는 경우 `control.json` 배포 구성 파일에서 `allowNodeMetricsCollection` 및 `allowPodMetricsCollection`*을 `false`로 설정하면 기본 제공되는 Pod 및 호스트 노드 메트릭 수집을 해제할 수 있습니다. 

예를 들면 다음과 같습니다. 

```json
"security": {
  ...
  "allowPodMetricsCollection": true,
  "allowNodeMetricsCollection": true,
  ...
}
```

> [!NOTE]
> OpenShift 환경의 경우 기본 제공되는 배포 프로필에서 이 설정이 기본적으로 false로 설정됩니다. Pod 및 노드 메트릭을 수집하는 데 필요한 권한 있는 기능과 OpenShift에 권장되는 보안 컨텍스트는 ‘제한된’ 제약 조건을 기반으로 합니다.

권한 없는 컨테이너 외에도, CU5부터 컨테이너는 지원되는 모든 플랫폼에서 BDC의 모든 새 배포에 대해 기본적으로 루트가 아닌 사용자로 실행됩니다. SQL Server 2019 CU5 해당 이미지 태그를 사용하여 모든 새 배포에 이러한 기능을 사용할 수 있습니다. 기존의 CU5 이전 BDC 배포는 영향을 받지 않으며 해당 클러스터의 애플리케이션은 계속 루트 사용자로 실행됩니다.

## <a name="next-steps"></a>다음 단계
[Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)

[Deploy [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] on OpenShift](deploy-openshift.md)(OpenShift에 SQL Server 빅 데이터 클러스터 배포)

[보안 백서](https://aka.ms/sql-bdc-openshift-security)
