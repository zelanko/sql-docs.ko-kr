---
title: Jupyter Notebook 및 Azure Data Studio를 사용하여 클러스터 모니터링
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 Jupyter Notebook 및 Azure Data Studio를 사용하여 클러스터를 모니터링합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 516b1bb461e5927ff52f0cee79e48d9945e6da21
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378501"
---
# <a name="monitoring-cluster-with-notebooks"></a>Notebook을 사용하여 클러스터 모니터링

이 페이지는 SQL Server 빅 데이터 클러스터용 Notebook의 색인입니다. 이러한 실행 가능 Notebook(.ipynb)은 빅 데이터 클러스터 모니터링을 지원하기 위해 SQL Server 2019용으로 설계되었습니다.

각 Notebook은 자체 종속성을 확인하도록 설계되었습니다. **모든 셀 실행** 은 성공적으로 완료되거나 예외가 발생하며 누락된 종속성을 해결하기 위한 다른 Notebook에 대한 하이퍼링크 힌트를 제공합니다. 후속 Notebook에 대한 힌트 하이퍼링크를 따라 이동하여 **모든 셀 실행** 을 누르고, 성공하면 원래 Notebook으로 돌아가서 **모든 셀 실행** 을 다시 누릅니다.

모든 종속성이 설치되었지만 **모든 셀 실행** 이 실패한 경우 각 Notebook은 결과를 분석하고 가능한 경우 다른 Notebook에 대한 하이퍼링크 힌트를 생성하여 문제 해결을 추가로 지원합니다.


## <a name="monitoring-kubernetes"></a>Kubernetes 모니터링

이 섹션에는 `azdata` CLI(명령줄 인터페이스)를 사용하여 SQL Server 빅 데이터 클러스터에 대한 정보 및 상태를 가져오는 데 유용한 일련의 Notebook이 포함되어 있습니다.

|Name |설명 |
|---|---|---|---|
|TSG006 - 시스템 Pod 상태 가져오기|모든 시스템 Pod의 상태를 봅니다. |
|TSG007 - BDC Pod 상태 가져오기|빅 데이터 클러스터 Pod 상태를 봅니다.|
|TSG008 - 버전 정보 가져오기(Kubernetes)|Kubernetes 클러스터 정보를 가져옵니다.|
|TSG009 - 노드 가져오기(Kubernetes)|Kubernetes 컨텍스트를 가져옵니다. |
|TSG010 - 구성 컨텍스트 가져오기|DMV 쿼리를 사용하여 내부 쿼리 프로세서 오류에 대한 자세한 정보를 얻습니다.|
|TSG015 - BDC 서비스 보기(Kubernetes)|Kubernetes 클러스터에 배포된 BDC 클러스터의 서비스 상태를 가져옵니다. |
|TSG016 - BDC Pod 설명|Kubernetes 클러스터에 배포된 BDC의 Pod 상태를 가져옵니다. |
|TSG020 - 노드 설명(Kubernetes)|BDC 클러스터에 대한 노드 정보를 가져옵니다(kubectl 명령줄 인터페이스를 사용). |
|TSG021 - 클러스터 정보 가져오기(Kubernetes)|Kubernetes 클러스터 정보를 가져옵니다. |
|TSG022 - kubeadm 호스트에 대한 외부 IP 주소 가져오기|kubeadm 호스트의 외부 IP 주소를 가져옵니다. |
|TSG023 - 모든 BDC 개체 가져오기(Kubernetes)|시스템 네임스페이스 및 빅 데이터 클러스터 네임스페이스에 대한 모든 Kubernetes 리소스의 요약 정보를 가져옵니다. |
|TSG042 - 노드 이름과 데이터 및 로그 PVC용 외부 탑재 가져오기|데이터 및 로그 외부 탑재와 함께 Pod를 호스트하는 노드 이름을 가져옵니다. |
|TSG063 - 스토리지 클래스 가져오기(Kubernetes)|이 Notebook을 사용하여 Kubernetes 스토리지 클래스를 가져옵니다. |
|TSG064 - BDC 영구적 볼륨 클레임 가져오기|빅 데이터 클러스터의 PVC(영구적 볼륨 클레임)을 표시합니다. |
|TSG065 - BDC 비밀 가져오기(Kubernetes)|빅 데이터 클러스터 비밀을 봅니다. |
|TSG066 - BDC 이벤트 가져오기(Kubernetes)|빅 데이터 클러스터 이벤트를 봅니다.|
|TSG072 - 영구적 볼륨 가져오기(Kubernetes)|Kubernetes 클러스터에 대한 PV(영구적 볼륨)를 표시합니다. 영구적 볼륨은 비 네임스페이스 개체입니다. |
|TSG081 - 네임스페이스 가져오기(Kubernetes)|Kubernetes 네임스페이스를 가져옵니다. |
|TSG089 - BDC 비 실행 Pod 설명|Kubernetes 클러스터의 비 실행 BDC Pod를 표시합니다. |
|TSG097 - BDC 상태 저장 세트 가져오기(Kubernetes)|Kubernetes 클러스터의 BDC 상태 저장 세트를 표시합니다. |
|TSG098 - BDC 복제본 세트 가져오기(Kubernetes)|Kubernetes 클러스터의 BDC 복제본 세트를 표시합니다. |
|TSG099 - BDC daemonset 가져오기(Kubernetes)|Kubernetes 클러스터의 BDC daemonset를 표시합니다. |


## <a name="monitor-big-data-cluster-bdc"></a>BDC(빅 데이터 클러스터) 모니터링

이 섹션에는 SQL Server BDC(빅 데이터 클러스터)를 호스트하는 Kubernetes 클러스터에 대한 정보 및 상태를 가져오는 데 유용한 일련의 Notebook이 포함되어 있습니다.

|Name |설명 |
|---|---|---|---|
|TSG003 - BDC Spark 세션 표시|BDC Spark 세션을 봅니다. |
|TSG004 - BDC 앱 표시|BDC 클러스터에서 실행 중인 앱을 봅니다.|
|TSG012 - BDC 상태 표시|BDC 클러스터의 다양한 구성 요소의 현재 상태를 가져옵니다.|
|TSG013 - 스토리지 풀 파일 목록 표시(HDFS)|스토리지 풀의 파일 목록을 가져옵니다(HDFS). |
|TSG014 - BDC 엔드포인트 표시|BDC 클러스터에 사용할 수 있는 모든 엔드포인트를 가져옵니다.|
|TSG017 - BDC 구성 표시|BDC 구성을 가져옵니다. |
|TSG033 - BDC SQL 상태 표시|Kubernetes 클러스터에 배포된 BDC의 SQL Server 상태를 가져옵니다. |
|TSG049 - BDC 컨트롤러 상태 표시|Kubernetes 클러스터에 배포된 BDC의 컨트롤러 상태를 가져옵니다. |
|TSG068 - BDC HDFS 상태 표시|Kubernetes 클러스터에 배포된 BDC의 HDFS 상태를 가져옵니다. |
|TSG069 - 빅 데이터 클러스터 게이트웨이 상태 표시|Kubernetes 클러스터에 배포된 BDC의 BDC 게이트웨이 상태를 가져옵니다. |
|TSG070 - SQL Master 풀 쿼리| 마스터 인스턴스에서 SQL 쿼리를 실행합니다. |

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
