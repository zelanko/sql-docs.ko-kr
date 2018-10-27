---
title: SQL Server 빅 데이터 클러스터에 대 한 보안 개념 | Microsoft Docs
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터에 대 한 보안 개념을 설명 합니다.
author: nelgson
ms.author: negust
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 77ffea6b2507bde65b914c52eaf225e1fd1dbd31
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050885"
---
# <a name="security-concepts-for-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터에 대 한 보안 개념

보안 빅 데이터 클러스터에서 HDFS/Spark 및 SQL Server 인증 및 권한 부여 시나리오에 대 한 일관적이 고 일관 된 지원을 의미합니다. 인증은 사용자 또는 서비스의 id를 확인 하 고 주장 하는 이러한가 프로세스입니다. 권한 부여 권한을 부여 하거나 요청 하는 사용자의 id를 기준으로 특정 리소스에 대 한 액세스 거부를 가리킵니다. 사용자 인증을 통해 식별 되 면이 단계가 수행 됩니다.

일반적으로 빅 데이터 컨텍스트에서 권한 부여가 특정 권한을 가진 사용자 id를 연결 하는 액세스 제어 목록 (Acl)을 통해 수행 됩니다. HDFS는 서비스 Api, HDFS 파일 및 작업 실행에 대 한 액세스를 제한 하 여 권한 부여를 지원 합니다.

이 문서에서는 빅 데이터 클러스터의 주요 보안 관련 개념을 설명 합니다.

## <a name="cluster-endpoints"></a>클러스터 끝점

빅 데이터 클러스터에 세 개의 진입점 가지

* HDFS/Spark (Knox) 게이트웨이 – HTTPS 기반 끝점입니다. 다른 끝점은이 통해 프록시입니다. HDFS/Spark 게이트웨이 webHDFS Livy와 같은 서비스에 액세스 하기 위해 사용 됩니다. Knox에 대 한 참조를 어디서 나 끝점입니다.

* 컨트롤러 끝점-클러스터를 관리 하기 위한 REST Api를 노출 하는 빅 데이터 클러스터 관리 서비스입니다. 관리 포털와 같은 일부 도구를이 끝점을 통해 액세스도 됩니다.

* 마스터 인스턴스-데이터베이스 도구 및 클러스터에서 SQL Server 마스터 인스턴스에 연결할 응용 프로그램에 대 한 TDS 끝점입니다.

![클러스터 끝점](media/concept-security/cluster_endpoints.png)

현재 외부에서 클러스터에 액세스 하기 위한 추가 포트를 열면의 방법이 있습니다.

### <a name="how-endpoints-are-secured"></a>끝점의 보안을 유지 하는 방법

완료 되는 빅 데이터 클러스터 끝점 보안을 설정 될 수 있는 암호를 사용 하 여 설정/업데이트 하거나 환경 변수 또는 CLI 명령을 사용 하 여 합니다. 모든 클러스터 내부 암호 Kubernetes 비밀로 저장 됩니다.  

# <a name="authentication"></a>인증

클러스터를 프로 비전 시 다양 한 로그인이 생성 됩니다.

이러한 로그인의 일부 서비스가 서로 통신할 수에 대 한 되며 다른 클러스터에 액세스 하는 최종 사용자에 대 한 합니다.

## <a name="end-user-authentication"></a>최종 사용자 인증
클러스터를 프로 비전 시 최종 사용자 암호의 수를 환경 변수를 사용 하 여 설정 해야 합니다. 다음은 SQL 관리자와 클러스터 관리자를 사용 하 여 서비스에 액세스 하는 암호입니다.

컨트롤러 사용자 이름:
 + CONTROLLER_USERNAME < controller_username > =

컨트롤러 암호:  
 + CONTROLLER_PASSWORD < controller_password > =

SQL Master SA 암호: 
 + MSSQL_SA_PASSWORD < controller_sa_password > =

HDFS/Spark 끝점에 액세스 하기 위한 암호:
 + KNOX_PASSWORD < knox_password > =

## <a name="intra-cluster-authentication"></a>내 클러스터 인증

 클러스터의 배포를 기반으로 다양 한 SQL 로그인 생성 됩니다.

* 특수 SQL 로그인은 시스템에서 sysadmin 역할을 사용 하 여 관리 하는 컨트롤러 SQL 인스턴스에 만들어집니다. 이 로그인에 대 한 암호 K8s 암호로 캡처됩니다.

* Sysadmin 로그인 컨트롤러 소유 하 고 관리 하는 클러스터의 모든 SQL 인스턴스에서 만들어집니다. 이러한 인스턴스에서 HA 설치 나 업그레이드 등의 관리 태스크를 수행 하는 컨트롤러에 대 한 필요 합니다. 이러한 로그인도 데이터 풀과 통신 하는 SQL 마스터 인스턴스와 같은 SQL 인스턴스 간에 클러스터 간 통신에 사용 됩니다.

> [!NOTE]
> CTP2.0, 기본 인증만 지원 됩니다. HDFS 개체 및 SQL-빅 데이터 클러스터 계산 및 데이터 풀에 대 한 세분화 된 액세스 제어는 아직 제공 되지 않습니다.

## <a name="intra-cluster-communication"></a>클러스터 내 통신

Livy Spark 또는 저장소 풀에는 Spark와 같은 빅 데이터 클러스터에 속한 SQL이 아닌 서비스와의 통신에 인증서를 사용 하 여 보안이 설정 됩니다. 모든 SQL 서버와 SQL Server 간 통신은 SQL 로그인을 사용 하 여 보호 됩니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 문서를 참조 합니다.

- [SQL Server 2019 빅 데이터 클러스터는 무엇 인가요?](big-data-cluster-overview.md)
- [빠른 시작: SQL Server 빅 데이터 클러스터의 kubernetes 배포](quickstart-big-data-cluster-deploy.md)
