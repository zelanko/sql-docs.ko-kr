---
title: BDC(빅 데이터 클러스터)용 관리 리소스
titleSuffix: SQL Server
description: 이 문서에서는 Azure Data Studio, Notebook 및 Azure Data CLI(azdata) 명령을 사용하여 빅 데이터 클러스터의 상태를 보는 방법을 설명합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 10/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d469d1b8d89b07748485c9df3f7f7905af52099
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358231"
---
# <a name="administration-resources-for-big-data-clusters-bdc"></a>BDC(빅 데이터 클러스터)용 관리 리소스 

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 외부에서 SQL Server 빅 데이터 클러스터를 관리하는 방법을 설명합니다.

## <a name="know-your-architecture"></a>아키텍처 이해

SQL Server 2019(15.x)부터 SQL Server 빅 데이터 클러스터에서는 Kubernetes에서 실행되는 SQL Server, Spark 및 HDFS 컨테이너의 확장 가능한 클러스터를 배포할 수 있습니다. 다음 문서에서는 빅 데이터 클러스터의 개요를 소개합니다.
- [SQL Server 빅 데이터 클러스터란 무엇인가요?](big-data-cluster-overview.md)

SQL Server 빅 데이터 클러스터는 균일하고 일관적인 권한 부여 및 인증을 제공합니다. 다음 문서에서는 빅 데이터 클러스터 보안의 개요를 소개합니다.
- [SQL Server 빅 데이터 클러스터의 보안 개념](concept-security.md)

## <a name="manage-and-operate-with-tools"></a>도구를 사용한 관리 및 운영

다음 문서에서는 다음과 같은 방법으로 빅 데이터 클러스터를 관리하고 운영하는 방법을 설명합니다. 

- [Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)
- [SQL Server 컨트롤러 대시보드의 빅 데이터 클러스터 관리](manage-with-controller-dashboard.md)
- [Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 관리](notebooks-manage-bdc.md)
- [Notebook을 사용하여 BDC(빅 데이터 클러스터) 관리](cluster-manage-notebooks.md)
- [Spark를 사용하여 샘플 Notebook 실행](notebooks-tutorial-spark.md)

## <a name="monitor-with-tools"></a>도구를 사용하여 모니터링

다음 문서에서는 다음과 같은 방법으로 빅 데이터 클러스터를 모니터링하는 방법을 설명합니다. 

- [Azure Data Studio를 사용하여 BDC 클러스터 모니터링](cluster-monitor-ads.md)
- [azdata 유틸리티를 사용하여 BDC 클러스터 모니터링](cluster-monitor-cmdlet.md)
- [Grafana 대시보드를 사용하여 BDC 클러스터 모니터링](cluster-monitor-grafana.md)
- [Juypter Notebook 및 Azure Data Studio를 사용하여 BDC 클러스터 모니터링](cluster-monitor-notebooks.md)

## <a name="monitor-and-inspect-logs-with-notebooks"></a>Notebook을 사용하여 로그 모니터링 및 검사

다음 문서에는 Azure Data Studio에서 사용할 수 있는 여러 Jupyter Notebook이 나열되어 있습니다.

- [Notebook을 사용하여 클러스터 모니터링](cluster-monitor-notebooks.md)
- [Notebook을 사용하여 클러스터에서 로그 수집 및 분석](cluster-logging-notebooks.md)

## <a name="big-data-clusters-troubleshooting-resources"></a>빅 데이터 클러스터 문제 해결 리소스

다음 문서에서는 빅 데이터 클러스터 문제를 해결하는 방법을 설명합니다.

- [kubectl 유틸리티를 사용하여 BDC 클러스터 문제 해결](cluster-troubleshooting-commands.md) 
- [pyspark Notebook 문제 해결](troubleshoot-pyspark-notebook.md)
- [Juypter Notebook 및 Azure Data Studio(ADS)를 사용하여 BDC 클러스터 문제 해결](cluster-troubleshooter-notebooks.md)
- [HDFS 사용 권한 복원](troubleshoot-hdfs-restore-admin.md)

다음 문서에서는 Active Directory 모드에서 배포된 빅 데이터 클러스터의 문제를 해결하는 방법을 설명합니다.
- [Active Directory 모드에서 BDC 클러스터 문제 해결](troubleshoot-active-directory.md) 
- [AD 모드 로그인 실패 문제 해결](troubleshoot-ad-login-failed-untrusted-domain.md)
- [BDC AD 모드 배포 중지 문제 해결](troubleshoot-ad-reverse-lookup-zone.md)

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]란?](big-data-cluster-overview.md)을 참조하세요.