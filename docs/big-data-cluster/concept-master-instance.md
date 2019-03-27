---
title: 마스터 인스턴스란 무엇 인가요?
titleSuffix: SQL Server 2019 big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 SQL Server 마스터 인스턴스를 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 9c3809e481e00c94f01c1968a82638df3e37f80f
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58477949"
---
# <a name="what-is-the-master-instance-in-a-sql-server-2019-big-data-cluster"></a>SQL Server 2019 빅 데이터 클러스터에 마스터 인스턴스란 무엇 인가요?

이 문서에서는의 역할을 설명 합니다 *SQL Server 마스터 인스턴스* SQL Server 2019 빅 데이터 클러스터에. 마스터 인스턴스는 SQL Server 빅 데이터 클러스터에서 실행 되는 SQL Server 인스턴스에 [제어 평면](big-data-cluster-overview.md#controlplane)합니다.

SQL Server 마스터 인스턴스는 다음 기능을 제공합니다.

## <a name="connectivity"></a>연결

SQL Server 마스터 인스턴스는 클러스터 외부에서 액세스할 수 있는 TDS 끝점을 제공합니다. 응용 프로그램 또는 Azure Data Studio와 같은 SQL Server 도구를 연결할 수 있습니다 또는 SQL Server Management Studio 이전과 같이이 끝점에 다른 SQL Server 인스턴스.

## <a name="scale-out-query-management"></a>스케일 아웃 쿼리 관리

SQL Server 마스터 인스턴스 노드를 SQL Server 인스턴스 간에 쿼리를 분산 하는 데 사용 되는 스케일 아웃 쿼리 엔진을 포함 합니다 [풀 계산](concept-compute-pool.md)합니다. 또한 스케일 아웃 쿼리 엔진 추가 구성 없이 클러스터의 모든 Hive 테이블에 대 한 transact-sql 액세스를 제공합니다.

## <a name="metadata-and-user-databases"></a>메타 데이터와 사용자 데이터베이스

표준 SQL Server 시스템 데이터베이스 외에도 SQL 마스터 인스턴스 또한 다음과 같은 항목이 포함

- HDFS 테이블 메타 데이터를 보유 하는 메타 데이터 데이터베이스
- 데이터 평면 분할 된 데이터베이스 맵
- 클러스터 데이터 평면에 대 한 액세스를 제공 하는 외부 테이블의 세부 정보입니다.
- PolyBase 외부 데이터 원본 및 사용자 데이터베이스에 정의 된 외부 테이블입니다.

사용자 고유의 사용자 데이터베이스를 SQL Server 마스터 인스턴스를 추가할 수도 있습니다.

## <a name="machine-learning-services"></a>Machine learning 서비스

SQL Server machine learning 서비스는 데이터베이스 엔진, SQL Server에서 Java, R 및 Python 코드를 실행 하는 데에 추가 기능입니다. 이 기능은 핵심 엔진 프로세스의 외부 프로세스를 격리 하지만 저장된 프로시저, R 또는 Python 문이 포함 된 T-SQL 스크립트 또는 Java R 관계형 데이터와 완벽 하 게 통합 되는 SQL Server 확장성 프레임 워크 기반 또는 T-SQL을 포함 하는 Python 코드입니다.

SQL Server 빅 데이터 클러스터의 일부로, machine learning 서비스는 기본적으로 SQL Server 마스터 인스턴스에서 제공 됩니다. 이 마스터 SQL Server 인스턴스에서 외부 스크립트 실행 활성화 되 면 이죠 Java sp_execute_external_script를 사용 하 여 R 및 Python 스크립트를 실행할 수를 의미 합니다.

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>빅 데이터 클러스터에 machine learning 서비스의 이점

SQL Server 2019 쉽게 일반적으로 엔터프라이즈 데이터베이스에 저장 하는 차원 데이터에 조인할 수는 빅 데이터에 대 한 합니다. 빅 데이터의 가치는 크게 조직 부분에만 되지 않지만 보고서, 대시보드 및 응용 프로그램에도 포함 되어 증가 합니다. 동시에 데이터 과학자를 Spark/HDFS 에코 시스템 도구를 사용 하 여 쉽게 액세스할 수 있는 외부 데이터 원본에는 SQL Server 마스터 인스턴스의 데이터에 대 한 실시간 액세스 계속할 수 _를 통해_ SQL Server 마스터 인스턴스입니다.

SQL Server 2019 빅 데이터 클러스터를 사용 하면 더에 엔터프라이즈 데이터 레이크를 사용 하 여 합니다. SQL Server 개발자 및 분석가 수 있습니다.

* Enterprise data lake의 데이터를 사용 하는 응용 프로그램을 빌드하십시오.
* TRANSACT-SQL 쿼리를 사용 하 여 모든 데이터에 대 한 설명입니다.
* SQL Server 도구 및 응용 프로그램의 기존 에코 시스템을 사용 하 여 액세스 하 고 엔터프라이즈 데이터를 분석.
* 데이터 가상화 및 데이터 마트를 통해 데이터 이동의 필요성을 줄입니다.
* 빅 데이터 시나리오에 대 한 Spark를 사용 하 여 계속 합니다.
* Spark 또는 SQL Server를 사용 하 여 data lake를 통해 모델을 학습 하는 지능형 엔터프라이즈 응용 프로그램을 빌드하십시오.
* 최상의 성능을 위해 프로덕션 데이터베이스에서 모델을 운영 합니다.
* 실시간 분석을 위한 엔터프라이즈 데이터 마트를 직접 Stream 데이터입니다.
* 시각적으로 대화식 분석 및 BI 도구를 사용 하 여 데이터를 탐색 합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
- [워크숍: Microsoft SQL Server 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
