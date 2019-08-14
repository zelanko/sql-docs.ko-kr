---
title: 보안 개념
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터(미리 보기)의 보안 개념을 설명합니다. 여기에는 클러스터 엔드포인트 및 클러스터 인증 설명이 포함됩니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 54ae86785590eb26fb8ac402f3ae8ab6c7f29a98
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958661"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터의 보안 개념

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

안전한 빅 데이터 클러스터는 SQL Server 및 HDFS/Spark 모두에서 인증 및 권한 부여 시나리오가 일관성 있게 지원됨을 의미합니다. 인증은 사용자 또는 서비스의 ID를 검증하고 본인이 맞는지 확인하는 프로세스입니다. 권한 부여는 요청하는 사용자의 ID에 따라 특정 리소스에 대한 액세스를 허용하거나 거부하는 작업을 말합니다. 이 단계는 인증을 통해 사용자를 확인한 후에 수행됩니다.

빅 데이터 컨텍스트의 권한 부여는 일반적으로 사용자 ID를 특정 사용 권한에 연결하는 ACL(액세스 제어 목록)을 통해 수행됩니다. HDFS는 서비스 API, HDFS 파일 및 작업 실행에 대한 액세스를 제한하여 권한 부여를 지원합니다.

이 문서에서는 빅 데이터 클러스터의 주요 보안 관련 개념을 설명합니다.

## <a name="cluster-endpoints"></a>클러스터 엔드포인트

빅 데이터 클러스터에 액세스하는 세 가지 진입점이 있습니다.

* HDFS/Spark(Knox) 게이트웨이 - HTTPS 기반 엔드포인트입니다. 다른 엔드포인트는 이 엔드포인트를 통해 프록시됩니다. HDFS/Spark 게이트웨이는 webHDFS, Livy 등의 서비스에 액세스하는 데 사용됩니다. Knox에 대한 참조가 표시되는 곳은 엔드포인트입니다.

* 컨트롤러 엔드포인트 - 클러스터를 관리하기 위한 REST API를 공개하는 빅 데이터 클러스터 관리 서비스입니다. 일부 도구도 이 엔드포인트를 통해 액세스합니다.

* 마스터 인스턴스 - 데이터베이스 도구 및 애플리케이션이 클러스터의 SQL Server 마스터 인스턴스에 연결하기 위한 TDS 엔드포인트입니다.

![클러스터 엔드포인트](media/concept-security/cluster_endpoints.png)

현재는 외부에서 클러스터에 액세스하기 위한 추가 포트를 열 수 있는 옵션이 없습니다.

### <a name="how-endpoints-are-secured"></a>엔드포인트의 보안 유지 방법

환경 변수 또는 CLI 명령을 사용하여 설정/업데이트할 수 있는 암호를 통해 빅 데이터 클러스터의 엔드포인트 보안을 유지합니다. 모든 클러스터 내부 암호는 Kubernetes 비밀에 저장됩니다.  

## <a name="authentication"></a>인증

클러스터 프로비저닝 시 다음과 같은 여러 가지 로그인이 생성됩니다.

일부 로그인은 서비스가 서로 통신하는 데 사용되고, 다른 로그인은 최종 사용자가 클러스터에 액세스하는 데 사용됩니다.

### <a name="end-user-authentication"></a>최종 사용자 인증
클러스터 프로비저닝 시 환경 변수를 사용하여 많은 최종 사용자 암호를 설정해야 합니다. SQL 관리자와 클러스터 관리자가 서비스에 액세스하는 데 사용하는 암호는 다음과 같습니다.

컨트롤러 사용자 이름:
 + CONTROLLER_USERNAME=<controller_username>

컨트롤러 암호:  
 + CONTROLLER_PASSWORD=<controller_password>

SQL 마스터 SA 암호: 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

HDFS/Spark 엔드포인트에 액세스하는 데 사용할 암호:
 + KNOX_PASSWORD=<knox_password>

### <a name="intra-cluster-authentication"></a>클러스터 내 인증

클러스터 배포 시 다음과 같은 여러 가지 SQL 로그인이 생성됩니다.

* 특수 SQL 로그인은 sysadmin 역할을 사용하여 시스템에서 관리되는 컨트롤러 SQL 인스턴스에 생성됩니다. 이 로그인의 암호는 K8s 비밀로 캡처됩니다.

* sysadmin 로그인은 컨트롤러가 소유하고 관리하는 클러스터의 모든 SQL 인스턴스에서 생성됩니다. 컨트롤러가 해당 인스턴스에서 HA 설정 또는 업그레이드와 같은 관리 작업을 수행하는 데 필요합니다. 이 로그인은 데이터 풀과 통신하는 SQL 마스터 인스턴스와 같은 SQL 인스턴스 간의 클러스터 내 통신에도 사용됩니다.

> [!NOTE]
> 현재 릴리스에서는 기본 인증만 지원됩니다. HDFS 개체 및 SQL 빅 데이터 클러스터 컴퓨팅 풀과 데이터 풀에 대한 세분화된 액세스 제어는 아직 제공되지 않습니다.

## <a name="intra-cluster-communication"></a>클러스터 내 통신

빅 데이터 클러스터에서 비 SQL 서비스와의 통신(예: Livy-Spark 또는 Spark-스토리지 풀)은 인증서를 사용하여 보안을 유지합니다. SQL Server 간의 모든 통신은 SQL 로그인을 사용하여 보안을 유지합니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [SQL Server 2019 빅 데이터 클러스터란?](big-data-cluster-overview.md)
- [워크샵: Microsoft SQL Server 빅 데이터 클러스터 아키텍처](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
