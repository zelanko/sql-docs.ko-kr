---
title: 보안 개념
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 빅 데이터 클러스터의 보안 개념을 설명합니다. 이 내용에는 클러스터 엔드포인트 및 클러스터 인증 설명이 포함됩니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7e3be3a3ea0d3f3b3d452bfea058ff85dd8a9141
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257253"
---
# <a name="security-concepts-for-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 보안 개념

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 빅 데이터 클러스터의 주요 보안 관련 개념을 설명합니다.

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]는 균일하고 일관적인 권한 부여 및 인증을 제공합니다. 기존 도메인에 대한 AD(Active Directory) 통합을 설정하는 완전히 자동화된 배포를 통해 빅 데이터 클러스터를 AD와 통합할 수 있습니다. AD 통합을 통해 빅 데이터 클러스터를 구성한 후에는 기존 ID 및 사용자 그룹을 활용하여 모든 엔드포인트에서 통합 액세스를 수행할 수 있습니다. 또한 SQL Server에서 외부 테이블을 만든 후에는 AD 사용자와 그룹에 외부 테이블에 대한 액세스 권한을 부여하여 데이터 원본에 대한 액세스를 제어할 수 있으므로, 데이터 액세스 정책을 단일 위치에 중앙 집중화할 수 있습니다.

이 비디오(14분)에서는 빅 데이터 클러스터 보안에 대한 개요를 제공합니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Security/player?WT.mc_id=dataexposed-c9-niner]


## <a name="authentication"></a>인증

외부 클러스터 엔드포인트는 AD 인증을 지원합니다. AD ID를 사용하여 빅 데이터 클러스터에 인증할 수 있습니다.

### <a name="cluster-endpoints"></a>클러스터 엔드포인트

빅 데이터 클러스터에 액세스하는 5개 진입점이 있습니다.

* 마스터 인스턴스 - SSMS 또는 Azure Data Studio 같은 데이터베이스 도구와 애플리케이션을 사용하여 클러스터의 SQL Server 마스터 인스턴스에 액세스할 수 있는 TDS 엔드포인트입니다. [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]에서 HDFS 또는 SQL Server 명령을 사용하는 경우 도구가 작업에 따라 다른 엔드포인트에 연결합니다.

* HDFS 파일, Spark(Knox)에 액세스하는 게이트웨이 - webHDFS 및 Spark와 같은 서비스에 액세스하기 위한 HTTPS 엔드포인트입니다.

* 클러스터 관리 서비스(컨트롤러) 엔드포인트 - 클러스터를 관리하기 위한 REST API를 공개하는 빅 데이터 클러스터 관리 서비스입니다. Azdata 도구를 사용하려면 이 엔드포인트에 연결해야 합니다.

* 관리 프록시 - 로그 검색 대시보드 및 메트릭 대시보드에 액세스하는 데 사용됩니다.

* 애플리케이션 프록시 - 빅 데이터 클러스터 내부에 배포된 애플리케이션을 관리하는 데 사용되는 엔드포인트입니다.

![클러스터 엔드포인트](media/concept-security/cluster_endpoints.png)

현재는 외부에서 클러스터에 액세스하기 위한 추가 포트를 열 수 있는 옵션이 없습니다.

## <a name="authorization"></a>권한 부여

클러스터 전체에서, Spark와 SQL Server에서 쿼리를 실행할 때 여러 구성 요소 간의 통합 보안을 통해 원래 사용자의 ID를 HDFS에 전달할 수 있습니다. 위에서 언급했듯이, 다양한 외부 클러스터 엔드포인트에서 AD 인증을 지원합니다.

클러스터에는 데이터 액세스를 관리하는 두 가지 수준의 권한 부여 검사가 있습니다. 빅 데이터 컨텍스트의 권한 부여는 SQL Server에서는 개체에 대한 기존 SQL Server 권한을 사용하여 수행되고, HDFS에서는 사용자 ID를 특정 권한과 연결하는 제어 목록(ACL)을 사용하여 수행됩니다.

안전한 빅 데이터 클러스터는 SQL Server 및 HDFS/Spark 모두에서 인증 및 권한 부여 시나리오가 일관성 있게 지원됨을 의미합니다. 인증은 사용자 또는 서비스의 ID를 검증하고 본인이 맞는지 확인하는 프로세스입니다. 권한 부여는 요청하는 사용자의 ID에 따라 특정 리소스에 대한 액세스를 허용하거나 거부하는 작업을 말합니다. 이 단계는 인증을 통해 사용자를 확인한 후에 수행됩니다.

빅 데이터 컨텍스트의 권한 부여는 사용자 ID를 특정 사용 권한에 연결하는 ACL(액세스 제어 목록)을 통해 수행됩니다. HDFS는 서비스 API, HDFS 파일 및 작업 실행에 대한 액세스를 제한하여 권한 부여를 지원합니다.

## <a name="encryption-in-flight-and-other-security-mechanisms"></a>전송 데이터 암호화 및 기타 보안 메커니즘

클라이언트 간의 통신을 외부 엔드포인트로 암호화하고, 클러스터 내 구성 요소 간의 통신은 인증서를 사용하여 TLS/SSL로 보호됩니다.

데이터 풀과 통신하는 SQL 마스터 인스턴스처럼 모든 SQL Server-SQL Server 간 통신은 SQL 로그인을 사용하여 보호됩니다.

> [!IMPORTANT]
>  빅 데이터 클러스터는 `etcd`를 사용하여 자격 증명을 저장합니다. 모범 사례로서, Kubernetes 클러스터가 `etcd` 미사용 데이터 암호화를 사용하도록 해야 합니다. 기본적으로 `etcd`에 저장된 비밀은 암호화되지 않습니다. Kubernetes 설명서에서는 이 관리 작업 https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/ 및 https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/ 에 대한 세부 정보를 제공합니다.

## <a name="data-encryption-at-rest"></a>휴지 상태의 암호화

SQL Server 빅 데이터 클러스터 미사용 데이터 암호화 기능에서는 SQL Server 및 HDFS 구성 요소에 대한 애플리케이션 수준 암호화의 핵심 시나리오를 지원합니다. 전체 기능 사용 가이드는[미사용 데이터 암호화 개념 및 구성 가이드](encryption-at-rest-concepts-and-configuration.md) 문서를 참조하세요.

> [!IMPORTANT]
> 볼륨 암호화는 모든 SQL Server 빅 데이터 클러스터 배포에 권장됩니다. Kubernetes 클러스터에서 구성된 고객 제공 스토리지 볼륨은 미사용 데이터 암호화에 대한 포괄적인 접근 방식으로 암호화되어야 합니다. SQL Server 빅 데이터 클러스터 미사용 데이터 암호화 기능은 추가 보안 계층으로, SQL Server 데이터 및 로그 파일의 애플리케이션 수준 암호화 및 HDFS 암호화 영역 지원을 제공합니다.


## <a name="basic-administrator-login"></a>기본 관리자 로그인

AD 모드에서 또는 기본 관리자 로그인만 사용하여 클러스터를 배포하도록 선택할 수 있습니다. 기본 관리자 로그인만 사용하는 것은 프로덕션 지원 보안 모드가 아니며, 제품 평가에 사용됩니다.

Active Directory 모드를 선택하더라도 클러스터 관리자에 대한 기본 로그인이 생성됩니다. 이 기능은 AD 연결이 중단되는 경우 대체 액세스를 제공합니다.

배포 시 이 기본 로그인에는 클러스터의 관리자 권한이 부여됩니다. 로그인 사용자는 SQL Server 마스터 인스턴스의 시스템 관리자이자 클러스터 컨트롤러의 관리자가 됩니다.
Hadoop 구성 요소는 혼합 모드 인증을 지원하지 않으므로, 기본 관리자 로그인을 사용하여 게이트웨이(Knox)를 인증할 수 없습니다.

배포 시 정의해야 하는 로그인 자격 증명은 다음과 같습니다.

클러스터 관리 사용자 이름:

 + `AZDATA_USERNAME=<username>`

클러스터 관리자 암호:  
 + `AZDATA_PASSWORD=<password>`

> [!NOTE]
> 비 AD 모드에서는 게이트웨이(Knox)를 인증하여 HDFS/Spark에 액세스하려면 위의 암호와 함께 사용자 이름을 사용해야 합니다. SQL Server 2019 CU5 이전에는 사용자 이름이 `root`입니다.
> 
> [!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

## <a name="next-steps"></a>다음 단계

[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)

[워크샵: Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)

[Kubernetes RBAC](kubernetes-rbac.md)
