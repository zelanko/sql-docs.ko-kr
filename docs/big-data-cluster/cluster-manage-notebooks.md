---
title: Jupyter Notebook 및 Azure Data Studio를 사용하여 BDC(빅 데이터 클러스터) 관리
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 Jupyter Notebook 및 Azure Data Studio를 사용하여 BDC(빅 데이터 클러스터)를 관리합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e549a8005144e85a20cf613ff6695d11f7ff030f
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378463"
---
# <a name="manage-big-data-clusters-bdc-the-cluster-with-notebooks"></a>Notebook을 사용하여 BDC(빅 데이터 클러스터) 관리

이 페이지는 SQL Server 빅 데이터 클러스터용 Notebook의 색인입니다. 이러한 실행 가능 Notebook(.ipynb)은 빅 데이터 클러스터 관리를 지원하기 위해 SQL Server 2019용으로 설계되었습니다.

각 Notebook은 자체 종속성을 확인하도록 설계되었습니다. **모든 셀 실행** 은 성공적으로 완료되거나 예외가 발생하며 누락된 종속성을 해결하기 위한 다른 Notebook에 대한 하이퍼링크 힌트를 제공합니다. 후속 Notebook에 대한 힌트 하이퍼링크를 따라 이동하여 **모든 셀 실행** 을 누르고, 성공하면 원래 Notebook으로 돌아가서 **모든 셀 실행** 을 다시 누릅니다.

모든 종속성이 설치되었지만 **모든 셀 실행** 이 실패한 경우 각 Notebook은 결과를 분석하고 가능한 경우 다른 Notebook에 대한 하이퍼링크 힌트를 생성하여 문제 해결을 추가로 지원합니다.


## <a name="installing-and-uninstalling-utilities-on-big-data-cluster-bdc"></a>BDC(빅 데이터 클러스터)에서 유틸리티 설치 및 제거

이 섹션에는 SQL Server 빅 데이터 클러스터를 관리하는 데 필요한 명령줄 도구 및 패키지를 설치/제거하는 데 유용한 일련의 Notebook 세트가 포함되어 있습니다.

|Name |설명 |
|---|---|---|---|
|SOP010 - 빅 데이터 클러스터 업그레이드|azdata를 사용하여 빅 데이터 클러스터를 업그레이드하려면 이 Notebook을 사용합니다. |
|SOP012 - Mac용 unixodbc 설치|Brew를 사용하여 SQL Server용 odbc를 설치하는 동안 오류가 발생하는 경우 이 Notebook을 사용합니다.|
|SOP036 - kubectl 명령줄 인터페이스 설치|OS에 관계없이 kubectl 명령줄 인터페이스를 설치하려면 이 Notebook을 사용합니다.|
|SOP037 - kubectl 명령줄 인터페이스 제거|OS에 관계없이 kubectl 명령줄 인터페이스를 제거하려면 이 Notebook을 사용합니다.|
|SOP038 - Azure 명령줄 인터페이스 설치|OS에 관계없이 Azure CLI 명령줄 인터페이스를 설치하려면 이 Notebook을 사용합니다.|
|SOP039 - Azure 명령줄 인터페이스 제거|OS에 관계없이 Azure CLI 명령줄 인터페이스를 제거하려면 이 Notebook을 사용합니다.|
|SOP040 - ADS Python 샌드박스에서 pip 업그레이드|ADS Python 샌드박스에서 pip를 업그레이드하려면 이 Notebook을 사용합니다.|
|SOP054 - azdata 명령줄 인터페이스 설치|OS에 관계없이 azdata 명령줄 인터페이스를 설치하려면 이 Notebook을 사용합니다.|
|SOP055 - azdata 명령줄 인터페이스 제거|OS에 관계없이 azdata 명령줄 인터페이스를 제거하려면 이 Notebook을 사용합니다.|
|SOP059 - Kubernetes Python 모듈 설치|Python을 사용하는 Kubernetes 모듈을 설치하려면 이 Notebook을 사용합니다.|
|SOP060 - Kubernetes 모듈 제거|Python을 사용하는 Kubernetes 모듈을 제거하려면 이 Notebook을 사용합니다.|
|SOP061 - 빅 데이터 클러스터 삭제|BDC 클러스터를 삭제하려면 이 Notebook을 사용합니다.|
|SOP062 - ipython-sql 및 pyodbc 모듈 설치|ipython-sql 및 pyodbc 모듈을 설치하려면 이 Notebook을 사용합니다.|
|SOP063 - azdata CLI(패키지 관리자 사용) 설치|패키지 관리자를 사용하는 azdata CLI를 설치하려면 이 Notebook을 사용합니다.|
|SOP064 - azdata CLI(패키지 관리자 사용) 제거|패키지 관리자를 사용하는 azdata CLI를 제거하려면 이 Notebook을 사용합니다.|
|SOP069 - SQL Server용 ODBC 설치|azdata의 일부 하위 명령에는 SQL Server ODBC 드라이버가 필요하므로 이 Notebook을 사용하여 ODBC 드라이버를 설치합니다.|


## <a name="managing-certificates-on-big-data-clusters-bdc"></a>BDC(빅 데이터 클러스터)에서 인증서 관리

빅 데이터 클러스터에서 인증서를 관리하기 위해 Notebook을 실행할 Notebook 집합입니다.

|Name |설명 |
|---|---|---|---|
|CER001 - 루트 CA 인증서 생성|루트 CA 인증서를 생성합니다. 이 기술은 이러한 클러스터에 연결하는 클라이언트에 업로드해야 하는 루트 CA 인증서의 수를 줄여주므로 각 환경의 모든 비프로덕션 클러스터에 대해 하나의 루트 CA 인증서를 사용하는 것이 좋습니다. |
|CER002 - 기존 루트 CA 인증서 다운로드|클러스터에서 생성된 루트 CA 인증서를 다운로드하려면 이 Notebook을 사용합니다.|
|CER003 - 기존 루트 CA 인증서 업로드|CER003 - 기존 루트 CA 인증서를 업로드합니다.|
|CER004 - 기존 루트 CA 인증서 다운로드 및 업로드|기존 루트 CA 인증서를 다운로드하고 업로드합니다. |
|CER010 - 생성된 루트 CA를 로컬로 설치|이 Notebook은 **CER001 - 루트 CA 인증서 생성** 또는 **CER003 - 기존 루트 CA 인증서 업로드** 를 사용하여 설치된 생성된 루트 CA 인증서를 빅 데이터 클러스터에서 로컬로 복사한 다음 이 컴퓨터의 로컬 인증서 저장소에 루트 CA 인증서를 설치합니다.|
|CER020 - 관리 프록시 인증서 만들기|이 Notebook은 관리 프록시 엔드포인트에 대한 인증서를 만듭니다.|
|CER021 - Knox 인증서 만들기|이 Notebook은 Knox 게이트웨이 엔드포인트에 대한 인증서를 만듭니다.|
|CER022 - 앱 프록시 인증서 만들기|이 Notebook은 앱 배포 프록시 엔드포인트에 대한 인증서를 만듭니다.|
|CER023 - 마스터 인증서 만들기|이 Notebook은 마스터 엔드포인트에 대한 인증서를 만듭니다.|
|CER030 - 생성된 CA를 사용하여 관리 프록시 인증서 서명|이 Notebook은 **CER001 - 루트 CA 인증서 생성** 또는 **CER003 - 기존 루트 CA 인증서 업로드** 를 사용하여 만들어진 생성된 루트 CA 인증서를 사용하여 **CER020 - 관리 프록시 인증서 만들기** 를 사용하여 만들어진 인증서에 서명합니다.|
|CER031 - 생성된 CA를 사용하여 Knox 인증서 서명|이 Notebook은 **CER001 - 루트 CA 인증서 생성** 또는 **CER003 - 기존 루트 CA 인증서 업로드** 를 사용하여 만들어진 생성된 루트 CA 인증서를 사용하여 **CER021 - Knox 인증서 만들기** 를 사용하여 만들어진 인증서에 서명합니다.|
|CER032 - 생성된 CA를 사용하여 앱 프록시 인증서 서명|이 Notebook은 **CER001 - 루트 CA 인증서 생성** 또는 **CER003 - 기존 루트 CA 인증서 업로드** 를 사용하여 만들어진 생성된 루트 CA 인증서를 사용하여 **CER022 - 앱 프록시 인증서 만들기** 를 사용하여 만들어진 인증서에 서명합니다.|
|CER033 - 생성된 CA를 사용하여 마스터 인증서 서명|이 Notebook은 **CER001 - 루트 CA 인증서 생성** 또는 **CER003 - 기존 루트 CA 인증서 업로드** 를 사용하여 만들어진 생성된 루트 CA 인증서를 사용하여 **CER023 - 마스터 인증서 만들기** 를 사용하여 만들어진 인증서에 서명합니다.|
|CER040 - 서명된 관리 프록시 인증서 설치|이 Notebook은 **CER030 - 생성된 CA를 사용하여 관리 프록시 인증서 서명** 을 사용하여 서명된 인증서를 빅 데이터 클러스터에 설치합니다.|
|CER041 - 서명된 Knox 인증서 설치|이 Notebook은 **CER031 - 생성된 CA를 사용하여 Knox 인증서 서명** 을 사용하여 서명된 인증서를 빅 데이터 클러스터에 설치합니다.|
|CER042 - 서명된 앱 프록시 인증서 설치|이 Notebook은 **CER032 - 생성된 CA를 사용하여 앱 프록시 인증서 서명** 을 사용하여 서명된 인증서를 빅 데이터 클러스터에 설치합니다.|
|CER043 - 서명된 컨트롤러 인증서 설치|이 Notebook은 **CER034 - 클러스터 루트 CA를 사용하여 컨트롤러 인증서 서명** 을 사용하여 서명된 인증서를 빅 데이터 클러스터에 설치합니다. 이 Notebook의 끝부분에서는 컨트롤러 Pod와 PolyBase를 사용하는 모든 Pod(마스터 풀 및 컴퓨팅 풀 Pod)를 다시 시작하여 새 인증서를 로드합니다.|
|CER050 - BDC가 정상 상태가 될 때까지 대기|이 Notebook은 새 인증서를 로드하기 위해 PolyBase를 사용하는 Pod가 다시 시작된 후 빅 데이터 클러스터가 정상 상태로 돌아갈 때까지 기다립니다.|
|CER100 - 자체 서명된 인증서를 사용하여 클러스터 구성|이 Notebook은 빅 데이터 클러스터에 새 루트 CA를 생성하고 각 엔드포인트에 대한 새 인증서를 만듭니다(해당 엔드포인트: 관리, 게이트웨이, 앱 프록시 및 컨트롤러). 컨트롤러 인증서(기존 클러스터 루트 CA를 사용하여 서명됨)를 제외하고 각각의 새 인증서를 새로 생성된 루트 CA로 서명하고 각 인증서를 빅 데이터 클러스터에 설치합니다. 이 컴퓨터의 신뢰할 수 있는 루트 인증 기관 인증서 저장소에 새로 생성된 루트 CA를 다운로드합니다. 생성된 자체 서명된 인증서는 모두 컨트롤러 Pod의 test_cert_store_root 위치에 저장됩니다.|
|CER101 - 기존 루트 CA를 사용하여 자체 서명된 인증서로 클러스터 구성|이 Notebook은 빅 데이터 클러스터에서 **CER003** 을 사용하여 업로드된 기존의 생성된 루트 CA를 사용하고 각 엔드포인트(관리, 게이트웨이, 앱 프록시 및 컨트롤러)에 대해 새 인증서를 만든 다음, 컨트롤러 인증서(기존 클러스터 루트 CA로 서명됨)를 제외한 각각의 새 인증서를 새로 생성된 루트 CA로 서명하고 각 인증서를 빅 데이터 클러스터에 설치합니다. 생성된 자체 서명된 인증서는 모두 컨트롤러 Pod에 저장됩니다(test_cert_store_root 위치). 이 Notebook이 완료되면 이 컴퓨터(및 새 루트 CA를 설치하는 모든 컴퓨터)에서 빅 데이터 클러스터로의 모든 https:// 액세스는 안전한 것으로 표시됩니다. Notebook Runner 챕터는 App-Deploy를 실행하도록 생성된 CronJob(OPR003)이 클러스터 루트 CA를 설치하여 안전하게 JWT 토큰 및 swagger.json을 가져올 수 있도록 합니다.|

## <a name="backup-and-restore-from-big-data-cluster-bdc"></a>BDC(빅 데이터 클러스터)로부터 백업 및 복원

이 섹션에는 SQL Server 빅 데이터 클러스터에 대한 백업 및 복원 작업에 유용한 일련의 Notebook이 포함되어 있습니다.

| Name | 설명 |
|--|--|
| SOP008 - distcp를 사용하여 Azure Data Lake Store Gen2에 HDFS 파일 백업 | 이 SOP(표준 작업 절차)는 원본 SQL Server 2019 BDC 클러스터의 HDFS 파일 시스템에서 지정된 Azure Data Lake Store Gen2 계정으로 데이터를 백업합니다. Azure Data Lake Store Gen2 계정이 "계층 구조 네임스페이스"를 사용하도록 구성되어 있는지 확인하세요. |

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
