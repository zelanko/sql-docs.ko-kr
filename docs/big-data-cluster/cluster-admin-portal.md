---
title: SQL Server 클러스터 관리 포털을 사용 하 여 빅 데이터 클러스터 (미리 보기) 모니터링 | Microsoft Docs
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 모니터링 하는 클러스터 관리 포털을 사용 하는 방법에 알아봅니다.
author: yualan
ms.author: alayu
manager: craigg
ms.date: 10/16/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 764e1689b4b793e3a993c058517a892f93d6d439
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356054"
---
# <a name="introduction-to-the-cluster-administration-portal"></a>클러스터 관리 포털 소개

모니터링 또는 SQL Server 2019 빅 데이터 클러스터 (미리 보기) 문제 해결 하려는 경우 클러스터 관리 포털을 사용 합니다.

클러스터 관리 포털을 사용 하면 수 있습니다.
- 신속 하 게 실행 되는 pod 및 문제 수를 보려면
- 배포 상태 모니터링
- 사용 가능한 서비스 끝점 보기
- 뷰 컨트롤러 및 SQL Server 마스터 인스턴스
- 드릴 다운 Grafana 대시보드 및 Kibana 로그에 액세스를 포함 하 여 pod에 대 한 정보

## <a name="access-the-cluster-administration-portal"></a>클러스터 관리 포털에 액세스

에 따라 합니다 [빅 데이터 클러스터를 배포 하는 빠른 시작](quickstart-big-data-cluster-deploy.md) 열릴 때까지 합니다 **클러스터 관리 포털** 섹션. Mssqlctl를 사용 하 여 실행 하는 빅 데이터 클러스터를 만든 후 다음이 지침을 따릅니다.

컨트롤러 pod가 실행 되 면 배포를 모니터링 하려면 클러스터 관리 포털을 사용할 수 있습니다. 외부 IP 주소 및 포트 번호를 사용 하 여 포털에 액세스할 수 있습니다 합니다 `service-proxy-lb` (예: **https://\<ip 주소\>: 30777**). 값은 관리 포털 액세스에 대 한 자격 증명 `CONTROLLER_USERNAME` 고 `CONTROLLER_PASSWORD` 위에 제공 된 환경 변수입니다.

> [!NOTE]
> CTP 2.0에 대 한 경우 보안 경고를 자동으로 생성 된 SSL 인증서 사용 하므로 웹 페이지에 액세스 하는 경우

## <a name="overview"></a>개요

![개요](./media/cluster-admin-portal/portal-overview.png)

포털을 처음 입력 하면 실행 되는 pod의 수를 신속 하 게 볼 수 있습니다.
- 컨트롤러
- 마스터 인스턴스
- 풀 계산
- 저장소 풀
- 데이터 풀

모든 문제가 있는 경우에 알려진된 문제에 대 한 링크를 열 수 있습니다. 문제가 발생 하는 경우 특정 풀으로 이동 하려면 왼쪽된 탐색 창에 사용할 수 있습니다.

## <a name="deployment"></a>배포

![배포](./media/cluster-admin-portal/portal-deployment.png)

배포를 모니터링 하려면 왼쪽의 [배포] 탭을 클릭 합니다. 배포의 트리 보기가 표시 수 및 배포에 문제가 있는 경우.

## <a name="service-endpoints"></a>서비스 끝점

![엔드포인트](./media/cluster-admin-portal/portal-endpoints.png)

왼쪽된 탐색 창에서 끝점 탭을 클릭 하 여 사용 가능한 서비스 끝점을 볼 수 있습니다.

이 Grafana 대시보드 Spark 끝점에 대 한 링크를 포함 하 고 Kibana 기록 합니다.

## <a name="controller"></a>컨트롤러

![컨트롤러](./media/cluster-admin-portal/portal-controller.png)

컨트롤러는 컨트롤러와 관련 된 모든 pod를 보여 줍니다. 컨트롤러에 대 한 자세히 알아볼 수 있습니다 [여기 있습니다.](concept-controller.md)

각 pod에 자세한 추가 정보를 알아보려면를 클릭할 수 있습니다 **메트릭을** Grafana 대시보드 보기에 열입니다.

문제를 사용 하 여 pod에 대 한 로그를 알아보려면 클릭할 수 있습니다 합니다 **로그** 열입니다.

## <a name="master-instance"></a>마스터 인스턴스

![엔드포인트](./media/cluster-admin-portal/portal-master.png)

마스터 인스턴스를 SQL Server 마스터 인스턴스와 관련 된 모든 pod를 보여 줍니다. 마스터 SQL Server 인스턴스에 대 한 자세히 알아볼 수 있습니다 [여기 있습니다.](concept-master-instance.md)

각 pod에 자세한 추가 정보를 알아보려면를 클릭할 수 있습니다 **메트릭을** Grafana 대시보드 보기에 열입니다.

문제를 사용 하 여 pod에 대 한 로그를 알아보려면 클릭할 수 있습니다 합니다 **로그** 열입니다.

## <a name="pool-and-pod-pages"></a>풀 및 Pod 페이지

![풀](./media/cluster-admin-portal/portal-data-pool.png)

모든 풀 페이지 (계산, 저장소 및 데이터)에서 드릴 다운할 수 있습니다 각 pod 페이지를 클릭 하 여 **기본**

![pod](./media/cluster-admin-portal/portal-data-default-pool.png)

드릴 다운 경로 맨 위에서 breadcrumb 보여 줍니다.

각 pod에 자세한 추가 정보를 알아보려면를 클릭할 수 있습니다 **메트릭을** Grafana 대시보드 보기에 열입니다.

문제를 사용 하 여 pod에 대 한 로그를 알아보려면 클릭할 수 있습니다 합니다 **로그** 열입니다.

각 풀에 대 한 자세한 내용을 보려면:
- [풀 계산](concept-compute-pool.md)
- [저장소 풀](concept-storage-pool.md)
- [데이터 풀](concept-data-pool.md)

## <a name="about-page"></a>페이지에 대 한

![정보](./media/cluster-admin-portal/portal-about.png)

여기 설명서의 다른 버전 번호, 컨테이너 및 링크와 같은 클러스터에 대 한 정보를 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

클러스터 관리 포털 외에도 클러스터의 상태를 탐색 하려면 몇 가지 유용한 Kubernetes 명령을 실행할 수도 있습니다. 자세한 내용은 [모니터링 및 SQL Server 빅 데이터 클러스터 문제 해결에 대 한 Kubectl 명령을](cluster-troubleshooting-commands.md)합니다.

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요 [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
