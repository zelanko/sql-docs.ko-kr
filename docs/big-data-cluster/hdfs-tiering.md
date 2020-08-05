---
title: HDFS 계층화 구성
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터의 HDFS에 외부 Azure Data Lake Storage 파일 시스템을 탑재하도록 HDFS 계층화를 구성하는 방법을 설명합니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60aa2f27f83b4b3e91f22e54cb85fa0794a5355f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730637"
---
# <a name="configure-hdfs-tiering-on-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에서 HDFS 계층화 구성

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

HDFS 계층화는 HDFS에서 외부 HDFS 호환 파일 시스템을 탑재하는 기능을 제공합니다. 이 문서에서는 SQL Server 빅 데이터 클러스터에 대해 HDFS 계층화를 구성하는 방법을 설명합니다. 현재, Azure Data Lake Storage Gen2 및 Amazon S3에 연결하도록 지원됩니다. 

## <a name="hdfs-tiering-overview"></a>HDFS 계층화 개요

계층화를 사용하는 경우 애플리케이션은 데이터가 로컬 HDFS에 있는 것처럼 다양한 외부 저장소의 데이터에 원활하게 액세스할 수 있습니다. 탑재는 외부 파일 시스템의 네임스페이스를 설명하는 메타데이터가 로컬 HDFS로 복사되는 메타데이터 작업입니다. 이 메타데이터에는 외부 디렉터리와 파일에 대한 정보와 해당 사용 권한 및 ACL이 포함됩니다. 예를 들어 쿼리를 통해 데이터 자체에 액세스하는 경우, 해당 데이터는 요청이 있을 때만 복사됩니다. 이제 SQL Server 빅 데이터 클러스터에서 외부 파일 시스템 데이터에 액세스할 수 있습니다. 클러스터의 HDFS에 저장된 로컬 데이터에 실행하는 것과 동일한 방식으로 이 데이터에 대해 Spark 작업 및 SQL 쿼리를 실행할 수 있습니다.

7분 분량의 다음 동영상에서는 HDFS 계층화의 개요를 제공합니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Unify-your-data-lakes-with-HDFS-tiering/player?WT.mc_id=dataexposed-c9-niner]


### <a name="caching"></a>캐싱
현재, 기본적으로 총 HDFS 스토리지의 1%가 탑재된 데이터의 캐싱용으로 예약됩니다. 캐싱은 탑재 전체의 전역 설정입니다.

> [!NOTE]
> HDFS 계층화는 Microsoft에서 개발한 기능이며, 이전 버전은 Apache Hadoop 3.1 배포의 일부로 출시되었습니다. 자세한 내용은 [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806)을 참조하세요.

다음 섹션에서는 Azure Data Lake Storage Gen2 데이터 원본을 사용하여 HDFS 계층화를 구성하는 방법의 예제를 제공합니다.

## <a name="refresh"></a>새로 고침

HDFS 계층화는 새로 고침을 지원합니다. 원격 데이터의 최신 스냅샷에 대한 기존 탑재를 새로 고칩니다.

## <a name="prerequisites"></a>사전 요구 사항

- [빅 데이터 클러스터 배포](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>탑재 지침

Azure Data Lake Storage Gen2 및 Amazon S3에 연결하도록 지원됩니다. 이러한 스토리지 유형에서 탑재하는 방법에 대한 지침은 다음 문서에서 찾을 수 있습니다.

- [빅 데이터 클러스터에 HDFS 계층화를 위한 ADLS Gen2를 탑재하는 방법](hdfs-tiering-mount-adlsgen2.md)
- [빅 데이터 클러스터에 HDFS 계층화를 위한 S3를 탑재하는 방법](hdfs-tiering-mount-s3.md)

## <a name="known-issues-and-limitations"></a><a id="issues"></a> 알려진 이슈 및 제한 사항

다음 목록은 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에서 HDFS 계층화를 사용하는 경우의 알려진 이슈 및 현재 제한 사항을 제공합니다.

- 탑재가 장시간 `CREATING` 상태로 중단되면 실패했을 가능성이 가장 높습니다. 이 경우 명령을 취소하고 필요한 경우 탑재를 삭제합니다. 매개 변수와 자격 증명이 올바른지 확인한 후 다시 시도합니다.

- 기존 디렉터리에는 탑재를 만들 수 없습니다.

- 기존 탑재 내에는 탑재를 만들 수 없습니다.

- 탑재 지점의 상위 항목이 없으면 기본값이 r-xr-xr-x (555)인 사용 권한으로 탑재가 만들어집니다.

- 탑재되는 파일의 수와 크기에 따라 탑재를 만드는 데 다소 시간이 걸릴 수 있습니다. 이 과정에서 탑재 중인 파일은 사용자에게 표시되지 않습니다. 탑재를 만드는 동안 모든 파일이 임시 경로(기본값: `/_temporary/_mounts/<mount-location>`)에 추가됩니다.

- 탑재 만들기 명령은 비동기식입니다. 명령을 실행한 후 탑재 상태를 확인하여 상황을 이해할 수 있습니다.

- 탑재를 만들 때 **--mount-path**에 사용되는 인수는 기본적으로 탑재의 고유 식별자입니다. 후속 명령에는 동일한 문자열(있는 경우 끝에 "/" 포함)을 사용해야 합니다.

- 탑재는 읽기 전용입니다. 탑재 아래에 디렉터리 또는 파일을 만들 수 없습니다.

- 변경될 수 있는 디렉터리와 파일은 탑재하지 않는 것이 좋습니다. 탑재를 만든 후에 원격 위치에 대한 변경이나 업데이트는 HDFS의 탑재에 반영되지 않습니다. 원격 위치에서 변경이 수행되면 업데이트된 상태를 반영하도록 탑재를 삭제했다가 다시 만들도록 선택할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
