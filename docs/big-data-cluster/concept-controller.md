---
title: 컨트롤러는 무엇입니까?
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 컨트롤러에 대해 설명 합니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e984c3dced4bde713ac98d67c22481e54491cd68
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419540"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 컨트롤러는 무엇 인가요?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

컨트롤러는 빅 데이터 클러스터를 배포 하 고 관리 하기 위한 핵심 논리를 호스팅합니다. 클러스터의 일부인 Kubernetes, SQL Server 인스턴스와 HDFS 및 Spark와 같은 기타 구성 요소와의 모든 상호 작용을 처리 합니다.

컨트롤러 서비스는 다음과 같은 핵심 기능을 제공 합니다.

- 클러스터 수명 주기 관리: 클러스터 부트스트랩 & 삭제, 업데이트 구성
- Master SQL Server 인스턴스 관리
- 계산, 데이터 및 저장소 풀 관리
- 클러스터의 상태를 관찰 하는 모니터링 도구를 제공 합니다.
- 문제 해결 도구를 노출 하 여 예기치 않은 문제 검색 및 복구
- 클러스터 보안 관리:
  - 보안 클러스터 끝점 확인
  - 사용자 및 역할 관리
  - 클러스터 간 통신을 위한 자격 증명 구성

## <a name="deploying-the-controller-service"></a>컨트롤러 서비스 배포

컨트롤러는 고객이 빅 데이터 클러스터를 빌드하려고 하는 동일한 Kubernetes 네임 스페이스에 배포 되 고 호스팅됩니다. 이 서비스는 **azdata** 명령줄 유틸리티를 사용 하 여 클러스터 부트스트랩 중에 Kubernetes 관리자가 설치 합니다. 자세한 내용은 [SQL Server 빅 데이터 클러스터 시작](deploy-get-started.md)을 참조 하세요.

Buildout 워크플로는 [개요](big-data-cluster-overview.md) 문서에 설명 된 모든 구성 요소를 포함 하는 완전 한 기능 SQL Server 빅 데이터 클러스터의 위에 레이아웃을 Kubernetes 합니다. 부트스트랩 워크플로는 컨트롤러 서비스를 먼저 만들며,이를 배포한 후에는 컨트롤러 서비스가 마스터, 계산, 데이터 및 저장소 풀의 나머지 서비스 부분을 설치 하 고 구성 하는 것을 조정 합니다.

## <a name="managing-the-cluster-through-the-controller-service"></a>컨트롤러 서비스를 통해 클러스터 관리

**Azdata** 명령 중 하나를 사용 하 여 컨트롤러 서비스를 통해 클러스터를 관리할 수 있습니다. Pod와 같은 추가 Kubernetes 개체를 동일한 네임 스페이스에 배포 하는 경우 해당 개체는 컨트롤러 서비스에 의해 관리 되거나 모니터링 되지 않습니다. **Kubectl** 명령을 사용 하 여 Kubernetes 수준에서 클러스터를 관리할 수도 있습니다. 자세한 내용은 [빅 데이터 클러스터 SQL Server 모니터링 및 문제 해결](cluster-troubleshooting-commands.md)을 참조 하세요.

빅 데이터 클러스터에 대해 만들어진 컨트롤러 및 Kubernetes 개체 (상태 저장 집합, pod, 암호 등)는 전용 Kubernetes 네임 스페이스에 상주 합니다. Kubernetes 클러스터 관리자가 해당 네임 스페이스 내의 모든 리소스를 관리할 수 있도록 컨트롤러 서비스에 권한이 부여 됩니다.  이 시나리오에 대 한 RBAC 정책은 **azdata**를 사용 하 여 초기 클러스터 배포의 일부로 자동으로 구성 됩니다.

### <a name="azdata"></a>azdata

**azdata** 는 Python으로 작성 된 명령줄 유틸리티로, 클러스터 관리자가 컨트롤러 서비스에서 노출 하는 REST api를 통해 빅 데이터 클러스터를 부트스트랩 하 고 관리할 수 있도록 합니다.

## <a name="controller-service-security"></a>컨트롤러 서비스 보안

컨트롤러 서비스에 대 한 모든 통신은 HTTPS를 통해 REST API를 통해 수행 됩니다. 부트스트랩 시 자체 서명 된 인증서가 자동으로 생성 됩니다. 

컨트롤러 서비스 끝점에 대 한 인증은 사용자 이름 및 암호를 기반으로 합니다. 이러한 자격 증명은 환경 변수 `CONTROLLER_USERNAME` 및 `CONTROLLER_PASSWORD`에 대 한 입력을 사용 하 여 클러스터 부트스트랩 시간에 프로 비전 됩니다.

> [!NOTE]
> [SQL Server 암호 복잡성 요구 사항을](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017)준수 하는 암호를 제공 해야 합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대해 자세히 알아보려면 다음 리소스를 참조 하세요.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
- [걸친 빅 데이터 클러스터 아키텍처 Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
