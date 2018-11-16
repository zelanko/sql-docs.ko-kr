---
title: SQL Server Always On 가용성 그룹 Kubernetes 연산자 글로벌 요구 사항
description: 이 문서는 SQL Server Kubernetes Always On 가용성 그룹 연산자 글로벌 요구 사항에 대 한 매개 변수를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cd3cf1cd36866010843347d5c7a05a8cd39c20ef
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660602"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On 가용성 그룹 Kubernetes 연산자 매개 변수

Always On 가용성 그룹에서 kubernetes는 연산자가 필요 합니다. 매니페스트는 연산자에 설명 합니다. 매니페스트는는 `.yaml` 파일입니다. 지정의 예제를 보려면 [SQL Server 컨테이너에 대 한 Always On 가용성 그룹](sql-server-ag-kubernetes.md)합니다.

이 문서에서는 연산자 전역 환경 변수를 설명 합니다.

## <a name="example"></a>예제

다음 예제에 대 한 배포에 설명 합니다 `mssql-operator`합니다.

## <a name="global-environment-variables"></a>전역 환경 변수

* `MSSQL_K8S_POD_NAMESPACE` 
  * 필수
  * **설명**: The Kubernetes 네임 스페이스 연산자입니다.

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * 선택 사항
  * **설명**: sql server 쓰기 임대 기간입니다. 쓰기 가능한 sql server를 유지 하 여 스플릿 브레인 시나리오를 방지 하는 데 사용 합니다. 보조 복제본이 새 리더를 선택한 후 초 동안 기다립니다.

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * 선택 사항
  * **설명**: 가용성 그룹의 상태를 모니터링 하는 기간. 복제본 추가 및 삭제 속도 결정 합니다. 해야 미만 `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`합니다.
  * **기본**: 1

* `MSSQL_K8S_LEASE_DURATION_SECONDS`
  * 선택 사항
  * **설명**: 가용성 그룹 리더가 임대 기간입니다. 보조 복제본은 다시 주 복제본에서 반복적인 충돌이 발생 하는 경우를 선택 하기 전에 대기 하는 기간을 결정 합니다. 이 SQL Server 쓰기 임대가 다릅니다. 
  * **기본**: 10
  
  >[!NOTE]
  >다른 설정을 자동으로 따라 계산 `MSSQL_K8S_LEASE_DURATION_SECONDS`합니다.

* `MSSQL_K8S_RENEW_DEADLINE_SECONDS`
  * 선택 사항
  * **설명**: 역할 주 복제본을 포기 하기 전에 새로 고침 리더십을 다시 시도 하는 기간. 해야 미만 `MSSQL_K8S_LEASE_DURATION_SECONDS`합니다.
  * **기본**:  `MSSQL_K8S_LEASE_DURATION_SECONDS` /2

* `MSSQL_K8S_RETRY_PERIOD_SECONDS`
  * 선택 사항
  * **설명을**: 기간 작동 하 [마스터](https://kubernetes.io/docs/concepts/architecture/master-node-communication/) 리더가 임대를 갱신 하기 전에 대기 합니다. 해야 미만 `MSSQL_K8S_LEASE_DURATION_SECONDS`합니다.
  * **기본**:  `MSSQL_K8S_RENEW_DEADLINE_SECONDS` /2

* `MSSQL_K8S_ACQUIRE_PERIOD_SECONDS` 
  * 선택 사항
  * **설명**: 리더 임대가 만료 된 경우 보조 복제본에서 폴링하는 기간. 
  * **기본**: 1


  ## <a name="next-steps"></a>다음 단계

[Kubernetes 클러스터에서 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)
