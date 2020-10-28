---
title: Jupyter Notebook 및 Azure Data Studio를 사용하여 로그 수집 및 분석
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 Jupyter Notebook 및 Azure Data Studio를 사용하여 클러스터를 로깅합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5efb20db2b0f5e3d3509715a8711ce32414fa9ee
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378474"
---
# <a name="gathering-and-analyzing-logs-in-the-cluster-with-notebooks"></a>Notebook을 사용하여 클러스터에서 로그 수집 및 분석

이 페이지는 SQL Server 빅 데이터 클러스터용 Notebook의 색인입니다. 이러한 실행 가능 Notebook(.ipynb)은 빅 데이터 클러스터 로깅을 지원하기 위해 SQL Server 2019용으로 설계되었습니다.

각 Notebook은 자체 종속성을 확인하도록 설계되었습니다. **모든 셀 실행** 은 성공적으로 완료되거나 예외가 발생하며 누락된 종속성을 해결하기 위한 다른 Notebook에 대한 하이퍼링크 힌트를 제공합니다. 후속 Notebook에 대한 힌트 하이퍼링크를 따라 이동하여 **모든 셀 실행** 을 누르고, 성공하면 원래 Notebook으로 돌아가서 **모든 셀 실행** 을 다시 누릅니다.

모든 종속성이 설치되었지만 **모든 셀 실행** 이 실패한 경우 각 Notebook은 결과를 분석하고 가능한 경우 다른 Notebook에 대한 하이퍼링크 힌트를 생성하여 문제 해결을 추가로 지원합니다.

## <a name="gathering-logs-from-big-data-cluster-bdc"></a>BDC(빅 데이터 클러스터)에서 로그 수집

이 섹션에는 SQL Server BDC(빅 데이터 클러스터)에서 로그를 가져오는 데 유용한 일련의 Notebook이 포함되어 있습니다.

| Name | 설명 |
|--|--|
| TSG001 - azdata copy-logs 실행 | azdata 명령줄 인터페이스를 사용하여 BDC 클러스터에서 데이터를 복사합니다. |
| TSG061 - BDC 네임스페이스의 Pod에 대한 모든 컨테이너 로그의 끝부분 가져오기 | 네임스페이스의 BDC 클러스터에서 Pod에 대한 모든 컨테이너 로그를 가져옵니다. |
| TSG062 - BDC 네임스페이스의 Pod에 대한 모든 이전 컨테이너 로그의 끝부분 가져오기 | 네임스페이스의 BDC 클러스터에서 Pod에 대한 이전의 컨테이너 로그를 모두 가져옵니다. |
| TSG083 - kubectl cluster-info dump 실행 | kubetl 명령줄 인터페이스를 사용하여 BDC 클러스터 관련 정보를 덤프합니다. |
| TSG084 - 내부 쿼리 프로세서 오류 | DMV 쿼리를 사용하여 내부 쿼리 프로세서 오류에 대한 자세한 정보를 얻습니다. |
| TSG091 - azdata CLI 로그 가져오기 | 로컬 머신에서 azdata 로그를 가져옵니다. |



## <a name="analyse-logs-from-big-data-clusters-bdc"></a>BDC(빅 데이터 클러스터)에서 로그 분석

SQL Server 빅 데이터 클러스터에서 로그를 수집하고 분석하는 Notebook 세트입니다.  분석 프로세스는 로그에서 발견된 알려진 문제에 대해 실행할 후속 Notebook을 제안합니다.

|Name|설명 |
|---|---|
|TSG030 - SQL Server 오류 로그 파일|SQL Server 오류 로그 파일을 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다. |
|TSG031 - SQL Server PolyBase 로그|SQL Server PolyBase 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG034 - Livy 로그|Livy 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG035 - Spark 기록 로그|Spark 기록 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG036 - 컨트롤러 로그|컨트롤러 로그의 마지막 'n'시간 분량을 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG046 - Knox 게이트웨이 로그|Knox는 클라이언트에 500 오류를 전달하고, 근본적인 이슈의 원인을 가리키는 세부 정보(스택)를 제거합니다. 따라서 이 Notebook을 사용하여 클러스터에서 Knox 로그를 가져오세요. Knox 게이트웨이 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG073 - InfluxDB 로그|InfluxDB 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG076 - 탄력적 검색 로그|탄력적 검색 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG077 - Kibana 로그|Kibana 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG088 - Hadoop datanode 로그|Hadoop 데이터 노드 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG090 - Yarn nodemanager 로그|Yarn nodemanager 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG092 - BDC에 있는 모든 컨테이너의 Supervisord 로그 뒷부분|BDC에 있는 모든 컨테이너의 Supervisord 로그 뒷부분을 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG093 - BDC에 있는 모든 컨테이너의 에이전트 로그 뒷부분|BDC에 있는 모든 컨테이너의 에이전트 로그 뒷부분을 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG094 - Grafana 로그|Grafana 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG095 - Hadoop namenode 로그|Hadoop 이름 노드 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|
|TSG096 - Zookeeper 로그|Zookeeper 로그를 가져오고 로그 항목을 분석하여 관련 문제 해결 가이드를 제안합니다.|

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
