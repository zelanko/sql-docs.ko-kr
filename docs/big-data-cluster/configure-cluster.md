---
title: 클러스터 구성
titleSuffix: Configure a SQL Server big data cluster
description: SQL Server 빅 데이터 클러스터를 구성하는 방법의 개요입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b75f6946af9a13d6a8202c627d4c24a2225a51c1
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549993"
---
# <a name="configure-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터 구성

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

배포 시 SQL Server 2019 빅 데이터 클러스터의 SQL Server 마스터 인스턴스, Apache Spark 및 Apache Hadoop에 대한 속성을 구성할 수 있습니다.

배포 후에는 빅 데이터 클러스터가 구성 속성 수정을 지원하지 않습니다.

## <a name="configuration-scopes"></a>구성 범위
빅 데이터 클러스터 구성에는 `service` 및 `resource`의 두 가지 범위 수준이 있습니다. 설정의 계층 구조도 이 순서에 따라 내림차순입니다. BDC 구성 요소는 가장 낮은 범위에서 정의된 설정 값을 사용합니다. 지정된 범위에 설정이 정의되지 않은 경우 상위의 부모 범위의 값을 상속합니다.

예를 들어 Spark 드라이버가 스토리지 풀 및 Sparkhead `resources`에서 사용할 기본 코어 수를 정의하는 것이 좋습니다. 다음 두 가지 방법으로 수행할 수 있습니다. 
- `Spark` 서비스 범위에서 기본 코어 값 지정  
- `storage-0` 및 `sparkhead` 리소스 범위에서 기본 코어 값 지정

첫 번째 시나리오에서 Spark 서비스(스토리지 풀 및 Sparkhead)의 모든 하위 범위 리소스는 Spark 서비스 기본값에서 기본 코어 수를 상속합니다.

두 번째 시나리오에서 각 리소스는 해당 범위에서 정의된 값을 사용합니다.

서비스 범위와 리소스 범위 모두에서 기본 코어 수가 구성된 경우 서비스 범위 값은 지정된 설정에서 가장 낮은 **사용자 구성** 범위이므로 리소스 범위 값이 서비스 범위 값을 재정의합니다.

구성에 대한 자세한 내용은 해당 문서를 참조하세요.

방법: 
- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 마스터 인스턴스 구성](configure-sql-server-master-instance.md)
- [빅 데이터 클러스터에서 Apache Spark 및 Apache Hadoop 구성](configure-spark-hdfs.md)

참조: 
- [SQL Server 마스터 인스턴스 구성 속성](reference-config-master-instance.md)
- [Apache Spark 및 Apache Hadoop(HDFS) 구성 속성](reference-config-spark-hadoop.md)
