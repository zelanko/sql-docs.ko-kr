---
title: Jupyter Notebook 및 Azure Data Studio를 사용하여 BDC(빅 데이터 클러스터) 문제 해결
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 Jupyter Notebook 및 Azure Data Studio를 사용하여 BDC 문제를 해결합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 073776c042c0a0da136347c8e1658603b755208f
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378469"
---
# <a name="troubleshooting-big-data-clusters-bdc-with-notebooks"></a>Notebook을 사용하여 BDC(빅 데이터 클러스터) 문제 해결

이 페이지는 SQL Server 빅 데이터 클러스터용 Notebook의 색인입니다. 이러한 실행 가능 Notebook(.ipynb)은 빅 데이터 클러스터 문제 해결을 지원하기 위해 SQL Server 2019용으로 설계되었습니다.

각 Notebook은 자체 종속성을 확인하도록 설계되었습니다. **모든 셀 실행** 은 성공적으로 완료되거나 예외가 발생하며 누락된 종속성을 해결하기 위한 다른 Notebook에 대한 하이퍼링크 힌트를 제공합니다. 후속 Notebook에 대한 힌트 하이퍼링크를 따라 이동하여 **모든 셀 실행** 을 누르고, 성공하면 원래 Notebook으로 돌아가서 **모든 셀 실행** 을 다시 누릅니다.

모든 종속성이 설치되었지만 **모든 셀 실행** 이 실패한 경우 각 Notebook은 결과를 분석하고 가능한 경우 다른 Notebook에 대한 하이퍼링크 힌트를 생성하여 문제 해결을 추가로 지원합니다.


## <a name="troubleshooting-big-data-cluster-bdc"></a>BDC(빅 데이터 클러스터) 문제 해결

이 섹션에는 SQL Server BDC(빅 데이터 클러스터)에서 로그를 가져오기 위한 일련의 Notebook이 포함되어 있습니다.

|Name |설명 |
|---|---|---|---|
|TSG100 - 빅 데이터 클러스터 문제 해결사|BDC(빅 데이터 클러스터) 문제 해결에 사용할 수 있는 모든 Notebook 및 사용 시기의 개요입니다.  |
|TSG101 - SQL Server 문제 해결사|SQL Server 문제 해결에 사용할 수 있는 모든 Notebook 및 사용 시기의 개요입니다.  |
|TSG102 - HDFS 문제 해결사|HDFS 문제 해결에 사용할 수 있는 모든 Notebook 및 사용 시기의 개요입니다.  |
|TSG103 - Spark 문제 해결사|Spark 문제 해결에 사용할 수 있는 모든 Notebook 및 사용 시기의 개요입니다.  |
|TSG104 - 컨트롤 문제 해결사|컨트롤러 문제 해결에 사용할 수 있는 모든 Notebook 및 사용 시기의 개요입니다.  |
|TSG105 - 게이트웨이 문제 해결사|Knox 게이트웨이 문제 해결에 사용할 수 있는 모든 Notebook 및 사용 시기의 개요입니다.  |
|TSG106 - 앱 문제 해결사|App-Deploy 문제 해결에 사용할 수 있는 모든 Notebook 및 사용 시기의 개요입니다.  |



## <a name="diagnose-issues-from-big-data-clusters-bdc"></a>BDC(빅 데이터 클러스터) 문제 진단

빅 데이터 클러스터에서 상황 및 상태를 진단하기 위한 일련의 Notebook입니다.

|Name |설명 |
|---|---|---|---|
|TSG002 - CrashLoopBackoff|이 TSG는 '실행 중' 상태로 전환하기 위한 마지막 시도가 실패한 각 컨테이너에 연결하여 현재 및 이전 컨테이너 로그를 가져옵니다. 이는 kubectl get Pod에 보고된 CrashLoopBackOff 문제를 디버그하는 데 유용합니다.|
|TSG025 - FSM 브라우저 - 쿼리 컨트롤러 FSM 상태|컨트롤러 데이터베이스에 연결하고 FSM(Finite State Machine) 상태를 검색하려면 이 Notebook을 사용합니다. 이 Notebook을 사용하여 활성 상태 머신을 나열하고 중단된 워크플로를 식별합니다.|
|TSG026 - 데이터 풀 노드에 연결(T-SQL을 실행하기 위해)|(T-SQL을 실행하기 위해) 데이터 풀 노드에 연결하려면 이 Notebook을 사용합니다.|
|TSG027 - 클러스터 배포 관찰|클러스터 배포를 관찰하려면 이 Notebook을 사용합니다. 이 Notebook은 SQL Server 빅 데이터 클러스터 만들기 문제를 해결하기 위한 지침을 제공하며, 다음 명령은 근본 원인을 정확히 파악하는 데 유용한 경우가 많습니다. |
|TSG029 - 클러스터에서 덤프 찾기|빅 데이터 클러스터의 SQL Server 또는 컨트롤러와 같은 프로세스에서 코어덤프 및 미니덤프를 찾으려면 이 Notebook을 사용합니다.|
|TSG032 - 모든 컨테이너에 대한 CPU 및 메모리 사용량|모든 컨테이너의 CPU 및 메모리 사용량을 확인하려면 이 Notebook을 사용합니다.|
|TSG037 - 주 복제본을 호스트하는 마스터 풀 Pod 확인|마스터 풀 고가용성을 사용하는 경우 빅 데이터 클러스터의 주 복제본을 호스트하는 마스터 풀 Pod를 확인하려면 이 Notebook을 사용합니다.|
|TSG044 - 마스터 풀 컨테이너에서 sqlcmd 실행|T-SQL을 통해 마스터 풀 노드에 직접 연결하려면 이 Notebook을 사용합니다.|
|TSG055 - sparkhead에 대한 curl 시간 측정|컨트롤러 Pod에서 sparkhead Pod까지의 curl 응답 시간을 이해하는 단계를 진단하려면 이 Notebook을 사용합니다.|
|TSG060 - 모든 BDC PVC의 영구적 볼륨 디스크 공간|각 컨테이너에 연결하고 BDC(빅 데이터 클러스터)의 각 PVC(영구적 볼륨 클레임)에 매핑된 각 PV(영구적 볼륨)에 사용되는/사용 가능한 디스크 공간을 가져오려면 이 Notebook을 사용합니다.|
|TSG078 - 클러스터가 정상임|BDC(빅 데이터 클러스터)가 정상 상태인지 확인하려면 이 Notebook을 사용합니다.|
|TSG079 - 컨트롤러 코어 덤프 생성|컨트롤러 코어 덤프를 생성하려면 이 Notebook을 사용합니다.|
|TSG086 - 모든 컨테이너에서 top 실행|모든 컨테이너에서 top을 실행하려면 이 Notebook을 사용합니다.|
|TSG087 - 이름 노드 Pod에서 hadoop fs CLI 사용|이름 노드 Pod에서 hadoop fs CLI를 사용하려면 이 Notebook을 사용합니다.|
|TSG108 - 컨트롤러 업그레이드 구성 맵 보기|**azdata bdc 업그레이드** 를 사용하여 빅 데이터 클러스터 업그레이드를 실행하는 경우 오류를 해결하려면 이 Notebook을 사용합니다.|
|TSG112 - Active Directory 배포 전 검사|BDC(빅 데이터 클러스터) 구성이 AD(Active Directory) 배포에 유효한지 검사하려면 이 Notebook을 사용합니다.|
|TSG115 - SQL Server on Linux 보안 로그 변환기|SQL Server on Linux용 secuirty.ldap 및 security.kerberos 로거에 의해 생성된 로그를 구문 분석하려면 이 Notebook을 사용합니다. 이러한 로거를 사용하려면 SQL Server on Linux를 실행하는 컴퓨터의 /var/opt/mssql/logger.ini에 아래 줄을 추가합니다. 참고: 이 파일은 대/소문자를 구분합니다.|
|TSG116 - SQL BDC 보안 지원 로그 변환기|SQL BDC에서 보안 지원 서비스로 생성된 로그를 구문 분석하려면 이 Notebook을 사용합니다. 로그를 가져오기 위해 클러스터에서 디버그 로그를 복사하여 압축을 풉니다. 아래 단계를 수행합니다. - "azdata bdc debug copy-logs -n <namespace> *"를 실행합니다. 그러면 여러 개의 .tar.gz 파일이 생성됩니다. - debuglogs-* <namespace>-<date>-<time>.tar.gz 파일의 내용을 추출합니다. - ./<namespace>/control-<…>/security-support/supervisol/log/secsupp-stderr---<…>.log에 저장된 보안 지원 로그를 찾습니다.|
|TSG119 - Active Directory 배포 후 검사|이 Notebook은 AD 배포 후에 BDC 구성의 유효성을 검사하도록 설계되었습니다. dnsName 특성을 사용하는 모든 엔드포인트에서 DNS 항목이 있는지 확인합니다. 이러한 DNS 항목은 별칭이 아닌 호스트 레코드(즉, CNAME 레코드가 아닌 레코드)여야 합니다. 또한 잘 알려진 AD 계정의 존재 여부 및 사용 여부와 예상된 SPN이 있는지 여부도 확인합니다.|






## <a name="repair-issues-from-big-data-clusters-bdc"></a>BDC(빅 데이터 클러스터)에서 복구 문제

SQL Server 빅 데이터 클러스터의 알려진 상황 및 상태를 복구하기 위한 일련의 Notebook입니다.

|Name |설명 |
|---|---|---|---|
|TSG005 - 전달 루프가 발견됨|감지된 전달 루프를 처리하려면 이 Notebook을 사용합니다. dnsmasq 유틸리티는 로컬 루프백을 resolv.conf에 배치할 수 있으며, 이렇게 하면 초기 클러스터 배포 중에 컨트롤러 Pod가 CrashLoopBackOff로 전환될 수 있기 때문입니다. https://askubuntu.com/questions/627899/nameserver-127-0-1-1-in-resolv-conf-wont-go-away|
|TSG011 - sparkhistory 서버 다시 시작|sparkhistory 서버를 다시 시작하려면 이 Notebook을 사용합니다. sparkhistory java 프로세스가 시작 중에 중지될 수 있기 때문입니다. sparkhistory 서버를 다시 시작하면(supervisorctl restart sparkhistory) 이 문제가 해결될 수 있습니다.|
|TSG018 - 마스터 풀에서 sqlservr 프로세스 종료| T-SQL SHUTDOWN이 ./sqlservr 프로세스를 재순환하지 않는 경우 이 Notebook을 사용합니다. 이 경우 이 Notebook을 사용하여 기본 sqlservr 프로세스를 종료하면 ./sqlservr 프런트 엔드 프로세스에서 자동으로 프로세스를 다시 시작합니다.|
|TSG024 - Namenode가 안전 모드| HDFS가 안전 모드로 전환될 때 이 Notebook을 사용합니다. 예를 들어 스토리지 풀에서 너무 많은 Pod가 너무 빨리 재순환되면 자동으로 안전 모드가 사용될 수 있습니다.|
|TSG028 - 모든 스토리지 풀 노드에서 노드 관리자 다시 시작| 모든 스토리지 풀 노드에서 노드 관리자를 다시 시작해야 하는 경우 이 Notebook을 사용합니다.|
|TSG038 - doc에 키가 없어서 BDC 만들기 실패| \- doc에 키가 없기 때문에 BDC에서 오류를 생성하는 경우 이 Notebook을 사용합니다.|
|TSG039 - 잘못된 개체 이름 ‘role_permissions’| Knox gateway.log에서 역할 권한으로 인한 잘못된 개체 문제가 있는 경우 이 Notebook을 사용합니다.|
|TSG040 - 오류가 발생하여 컨트롤러에서 파일 이름을 가져올 수 없음| 컨트롤러에서 파일 이름을 가져오는 동안 504 게이트웨이가 시간 초과되는 경우 이 Notebook을 사용합니다.|
|TSG041 - 새 비동기 I/O 컨텍스트를 만들 수 없음(sysctl fs.aio-max-nr 증가)| 새 비동기 I/O 컨텍스트를 만들 수 없는 경우(sysctl fs.aio-max-nr 증가) 이 Notebook을 사용합니다.|
|TSG045 - 이 크기의 VM에 연결할 수 있는 최대 데이터 디스크 수(AKS)| 이 크기의 VM에 연결할 수 있는 최대 데이터 디스크 수(AKS)에 도달한 경우 이 Notebook을 사용합니다.|
|TSG047 - ConfigException - 이름이 있는 개체가 하나만 필요| 이름이 있는 개체가 하나만 필요한 ConfigException을 사용하는 경우 이 Notebook을 사용합니다.|
|TSG048 - "컨트롤러 Pod가 준비되기를 기다리는 중"에서 배포가 중지됨| "컨트롤러 Pod가 준비되기를 기다리는 중"에서 배포가 중지되는 경우 이 Notebook을 사용합니다.|
|TSG050 - "timeout expired waiting for volumes to attach or mount for pod" 오류와 함께 클러스터 만들기가 중지됨| "timeout expired waiting for volumes to attach or mount for pod" 오류와 함께 클러스터 만들기가 중지되는 경우 이 Notebook을 사용합니다.|
|TSG052 - master-svc DNS를 가져오지 못했으며 다시 시도할 예정| "timeout expired waiting for volumes to attach or mount for pod" 오류와 함께 클러스터 만들기가 중지되는 경우 이 Notebook을 사용합니다.|
|TSG057 - 컨트롤러 서비스를 시작할 때 .System.TimeoutException 오류 발생| 컨트롤러 서비스를 시작할 때 System.TimeoutException 오류가 발생하는 경우 이 Notebook을 사용합니다.|
|TSG067 - kube 구성 설정을 완료할 수 없음| kube 구성 설정이 실패하는 경우 이 Notebook을 사용합니다.|
|TSG074 - 앱 배포 삭제| BDC 클러스터에서 앱을 삭제하는 데 문제가 있는 경우 이 Notebook을 사용합니다.|
|TSG075 - NetworkPlugin cni가 Pod를 설치할 수 없어 FailedCreatePodSandBox 발생| NetworkPlugin cni가 Pod를 설정하지 못해 FailedCreatePodSandBox 예외가 발생하는 경우 이 Notebook을 사용합니다.|
|TSG080 - azdata를 사용하여 Spark 세션 삭제| Spark 세션을 삭제하는 동안 문제가 발생하는 경우 이 Notebook을 사용합니다.|
|TSG109 - 업그레이드 시간 제한 설정| BDC 업그레이드 문제가 발생하는 경우 이 Notebook을 사용합니다.|
|TSG110 - Azdata에서 ApiError 반환| azdata가 ApiError를 반환하는 경우 이 Notebook을 사용합니다.|

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]란?](big-data-cluster-overview.md)을 참조하세요.

