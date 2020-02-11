---
title: 컨트롤러란?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 컨트롤러에 대해 설명합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 96a652a562ea5b38df593dc9642a46cd32c41f8b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73532409"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 컨트롤러란?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

컨트롤러는 빅 데이터 클러스터를 배포하고 관리하기 위한 핵심 논리를 호스트합니다. Kubernetes, 클러스터에 속한 SQL Server 인스턴스 및 기타 구성 요소(예: HDFS 및 Spark)와의 상호 작용을 모두 처리합니다.

컨트롤러 서비스는 다음과 같은 핵심 기능을 제공합니다.

- 클러스터 수명 주기 관리: 클러스터 부트스트랩 및 삭제, 업데이트 구성
- 마스터 SQL Server 인스턴스 관리
- 컴퓨팅 풀, 데이터 풀 및 스토리지 풀 관리
- 클러스터의 상태를 관찰하는 모니터링 도구 공개
- 예기치 않은 문제를 검색 및 복구하는 문제 해결 도구 공개
- 클러스터 보안 관리:
  - 클러스터 엔드포인트 보안 유지
  - 사용자 및 역할 관리
  - 클러스터 간 통신을 위한 자격 증명 구성

## <a name="deploying-the-controller-service"></a>컨트롤러 서비스 배포

컨트롤러는 고객이 빅 데이터 클러스터를 빌드하려는 동일한 Kubernetes 네임스페이스에 배포되고 호스트됩니다. 이 서비스는 클러스터 부트스트랩 중에 Kubernetes 관리자가 **azdata** 명령줄 유틸리티를 사용하여 설치합니다. 자세한 내용은 [시작[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-get-started.md)을 참조하세요.

빌드 워크플로는 [개요](big-data-cluster-overview.md) 문서에 설명된 모든 구성 요소를 포함하는 완전히 작동하는 SQL Server 빅 데이터 클러스터를 Kubernetes 위에 레이아웃합니다. 부트스트랩 워크플로는 먼저 컨트롤러 서비스를 만듭니다. 배포된 후에는 컨트롤러 서비스가 마스터, 컴퓨팅, 데이터 및 스토리지 풀의 나머지 서비스 부분에 대한 설치와 구성을 조정합니다.

## <a name="managing-the-cluster-through-the-controller-service"></a>컨트롤러 서비스를 통해 클러스터 관리

**azdata** 명령 중 하나를 사용하여 컨트롤러 서비스를 통해 클러스터를 관리할 수 있습니다. 동일한 네임스페이스에 Pod 등의 추가 Kubernetes 개체를 배포하는 경우 해당 개체는 컨트롤러 서비스에서 관리되거나 모니터링되지 않습니다. **kubectl** 명령을 사용하여 Kubernetes 수준에서 클러스터를 관리할 수도 있습니다. 자세한 내용은 [모니터링 및 문제 해결[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md)을 참조하세요.

빅 데이터 클러스터에 대해 만들어진 컨트롤러 및 Kubernetes 개체(상태 저장 세트, Pod, 비밀 등)는 전용 Kubernetes 네임스페이스에 상주합니다. Kubernetes 클러스터 관리자가 해당 네임스페이스의 모든 리소스를 관리할 수 있는 권한을 컨트롤러 서비스에 부여합니다.  이 시나리오에 대한 RBAC 정책은 최초 클러스터 배포 과정에서 **azdata**를 사용하여 자동으로 구성됩니다.

### <a name="azdata"></a>azdata

**azdata**는 Python으로 작성된 명령줄 유틸리티로, 클러스터 관리자가 컨트롤러 서비스에서 공개된 REST API를 통해 빅 데이터 클러스터를 부트스트랩하고 관리할 수 있도록 합니다.

## <a name="controller-service-security"></a>컨트롤러 서비스 보안

컨트롤러 서비스에 대한 모든 통신은 HTTPS를 통해 REST API를 사용하여 수행됩니다. 부트스트랩 시 자체 서명된 인증서가 자동으로 생성됩니다. 

컨트롤러 서비스 엔드포인트에 대한 인증은 Active Directory ID를 사용하거나 사용자 이름 및 암호를 기반으로 합니다. 이 자격 증명은 `AZDATA_USERNAME` 및 `AZDATA_PASSWORD` 환경 변수의 입력을 사용하여 클러스터 부트스트랩 시 프로비저닝됩니다.

> [!NOTE]
> [SQL Server 암호 복잡성 요구 사항](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017)을 준수하는 암호를 제공해야 합니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
- [워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
