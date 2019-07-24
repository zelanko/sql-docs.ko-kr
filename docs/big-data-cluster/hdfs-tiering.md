---
title: HDFS 계층화 구성
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 HDFS에 외부 Azure Data Lake Storage 파일 시스템을 탑재 하도록 HDFS 계층화를 구성 하는 방법을 설명 합니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17eedf9f0797a0adb5eda6ca8ee090fc762e1491
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419379"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터에서 HDFS 계층화 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 계층화는 HDFS에서 외부 HDFS 호환 파일 시스템을 탑재 하는 기능을 제공 합니다. 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 HDFS 계층화를 구성 하는 방법을 설명 합니다. 이번에는 Azure Data Lake Storage Gen2 및 Amazon s 3에 대 한 연결을 지원 합니다. 

## <a name="hdfs-tiering-overview"></a>HDFS 계층화 개요

계층화를 사용 하는 경우 응용 프로그램은 데이터가 로컬 HDFS에 있는 것 처럼 다양 한 외부 저장소의 데이터에 원활 하 게 액세스할 수 있습니다. 탑재는 외부 파일 시스템에서 네임 스페이스를 설명 하는 메타 데이터가 로컬 HDFS로 복사 되는 메타 데이터 작업입니다. 이 메타 데이터에는 외부 디렉터리와 파일에 대 한 정보와 해당 사용 권한과 Acl이 포함 됩니다. 예를 들어 쿼리를 통해 데이터에 액세스 하는 경우 해당 데이터는 주문형 으로만 복사 됩니다. 이제 SQL Server 빅 데이터 클러스터에서 외부 파일 시스템 데이터에 액세스할 수 있습니다. 클러스터의 HDFS에 저장 된 모든 로컬 데이터에서 실행 하는 것과 동일한 방식으로이 데이터에 대해 Spark 작업 및 SQL 쿼리를 실행할 수 있습니다.

### <a name="caching"></a>캐싱
현재는 기본적으로 총 HDFS 저장소의 1%가 탑재 된 데이터 캐싱에 예약 됩니다. 캐싱은 탑재 전체에 대 한 전역 설정입니다.

> [!NOTE]
> HDFS 계층화는 Microsoft에서 개발한 기능이 며, 이전 버전의 버전은 Apache Hadoop 3.1 배포의 일부로 출시 되었습니다. 자세한 내용은를 참조 [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806) 하십시오.

다음 섹션에서는 Azure Data Lake Storage Gen2 데이터 원본을 사용 하 여 HDFS 계층화를 구성 하는 방법의 예를 제공 합니다.

## <a name="refresh"></a>새로 고침

HDFS 계층화는 새로 고침을 지원 합니다. 원격 데이터의 최신 스냅숏에 대 한 기존 탑재를 새로 고칩니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>탑재 지침

Azure Data Lake Storage Gen2 및 Amazon s 3에 대 한 연결을 지원 합니다. 이러한 저장소 유형에 대해 탑재 하는 방법에 대 한 지침은 다음 문서에서 찾을 수 있습니다.

- [빅 데이터 클러스터에서 HDFS 계층화에 대 한 ADLS Gen2를 탑재 하는 방법](hdfs-tiering-mount-adlsgen2.md)
- [빅 데이터 클러스터에서 HDFS 계층화를 위해 S3을 탑재 하는 방법](hdfs-tiering-mount-s3.md)

## <a id="issues"></a>알려진 문제 및 제한 사항

다음 목록은 SQL Server 빅 데이터 클러스터에서 HDFS 계층화를 사용 하는 경우 알려진 문제 및 현재 제한 사항을 제공 합니다.

- 마운트가 `CREATING` 오랜 시간 동안 발생 하는 경우 실패 가능성이 가장 높습니다. 이 경우 명령을 취소 하 고 필요한 경우 탑재를 삭제 합니다. 매개 변수와 자격 증명이 올바른지 확인 한 후 다시 시도 하십시오.

- 기존 디렉터리에는 탑재를 만들 수 없습니다.

- 탑재는 기존 탑재 내에서 만들 수 없습니다.

- 탑재 지점의 상위 항목이 없으면 xr-xr (555)에 대 한 기본값을 사용 하 여 생성 됩니다.

- 탑재는 탑재 되는 파일의 수와 크기에 따라 다소 시간이 걸릴 수 있습니다. 이 과정에서 탑재 중인 파일은 사용자에 게 표시 되지 않습니다. 마운트가 생성 되는 동안 모든 파일이 임시 경로에 추가 됩니다 .이에 대 `/_temporary/_mounts/<mount-location>`한 기본값은입니다.

- 탑재 생성 명령은 비동기입니다. 명령을 실행 한 후 탑재 상태를 이해 하기 위해 탑재 상태를 확인할 수 있습니다.

- 탑재를 만들 때 **--mount 경로** 에 사용 되는 인수는 기본적으로 탑재의 고유 식별자입니다. 다음 명령에는 동일한 문자열 (끝에 "/" 포함)을 사용 해야 합니다.

- 탑재는 읽기 전용입니다. 탑재 중인 디렉터리 또는 파일을 만들 수 없습니다.

- 변경할 수 있는 디렉터리와 파일은 탑재 하지 않는 것이 좋습니다. 마운트가 생성 된 후 원격 위치에 대 한 변경 또는 업데이트는 HDFS의 탑재에 반영 되지 않습니다. 원격 위치에서 변경이 발생 하는 경우 업데이트 된 상태를 반영 하도록 탑재를 삭제 하 고 다시 만들도록 선택할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
