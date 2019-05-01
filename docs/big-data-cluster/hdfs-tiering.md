---
title: HDFS 계층 구성
titleSuffix: SQL Server big data clusters
description: 이 문서에는 HDFS에 계층화 (미리 보기)는 SQL Server 2019 빅 데이터 클러스터에서 HDFS에 외부 Azure 데이터 레이크 저장소 파일 시스템 탑재를 구성 하는 방법을 설명 합니다.
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ccafa7914d09971e33d60fc9d25c7b812983aa98
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472094"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터에 계층화 하는 HDFS 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS 계층화 할 수 있게 탑재 외부 HDFS 호환 파일 시스템 HDFS에 합니다. 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 계층화 HDFS 구성 하는 방법에 설명 합니다. 이때 Azure Data Lake 저장소 Gen2 및 Amazon S3 연결을 지원 합니다. 

## <a name="hdfs-tiering-overview"></a>HDFS 계층 개요

계층화 된 응용 프로그램 원활 하 게 데이터에에서 액세스할 수 다양 한 외부 저장소는 로컬 HDFS에 데이터가 있는 것 처럼 합니다. 탑재 하면 로컬 HDFS에 외부 파일 시스템에 네임 스페이스를 설명 하는 메타 데이터를 복사한 위치 메타 데이터 작업,입니다. 이 메타 데이터와 사용 권한 및 Acl 파일과 외부 디렉터리에 대 한 정보를 포함합니다. 예를 들어 쿼리를 통해 자체 데이터에 액세스 하는 경우 해당 데이터는만 복사 주문형 합니다. 외부 파일 시스템 데이터는 이제 SQL Server 빅 데이터 클러스터에서 액세스할 수 있습니다. 실행할 수 있습니다 Spark SQL 쿼리와 작업이이 데이터에 대해 실행 하는 해당 클러스터에서 HDFS에 저장 하는 로컬 데이터에 대해 동일한 방식.

### <a name="caching"></a>캐싱
현재 기본적으로 총 HDFS 저장소의 1% 탑재 된 데이터의 캐싱을 위해 예약 됩니다. 캐싱 탑재에서 전역 설정입니다.

> [!NOTE]
> 기능은 Microsoft에서 개발한 HDFS 계층화 및 Apache Hadoop 3.1 배포의 일부로 릴리스된 버전으로 합니다. 자세한 내용은 [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) 세부 정보에 대 한 합니다.

다음 섹션에서는 Azure Data Lake 저장소 Gen2 데이터 원본을 사용 하 여 계층화 하는 HDFS를 구성 하는 방법의 예제를 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a name="mounting-instructions"></a>탑재 지침

Azure Data Lake 저장소 Gen2 및 Amazon S3 연결을 지원 합니다. 다음 문서에서는 이러한 저장소 형식에 대해 탑재 하는 방법에 대 한 지침을 찾을 수 있습니다.

- [빅 데이터 클러스터에 계층화 하는 HDFS에 대 한 탑재 ADLS Gen2 하는 방법](hdfs-tiering-mount-adlsgen2.md)
- [빅 데이터 클러스터에 계층화 하는 HDFS에 대 한 탑재 S3 하는 방법](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> 알려진된 문제 및 제한 사항

SQL Server 빅 데이터 클러스터에 계층화 하는 HDFS를 사용 하는 경우 다음 목록에서는 알려진된 문제 및 현재 제한 사항:

- 에 걸려 탑재 하는 경우는 `CREATING` 가능성이 못했습니다 오랜 시간, 상태입니다. 이 경우 명령을 취소 하 고 필요한 경우 탑재를 삭제 합니다. 매개 변수 및 자격 증명 올바른지 확인 후 다시 시도 하세요.

- 기존 디렉터리의 탑재를 만들 수 없습니다.

- 기존 탑재 내 탑재를 만들 수 없습니다.

- 탑재 지점의 상위 항목 모두 존재 하지 않는 경우 만들어집니다 권한으로 r-xr-xr-x (555)를 기본값으로 합니다.

- 탑재 생성 되 고 탑재 된 파일의 크기와 수에 따라 다소 시간이 걸릴 수 있습니다. 이 과정에서 탑재에 있는 파일이 사용자에 게 보이지 않습니다. 모든 파일에 기본적으로 임시 경로 추가할 탑재를 만드는 동안 `/_temporary/_mounts/<mount-location>`합니다.

- 탑재 만들기 명령 비동기입니다. 명령이 실행 된 후 탑재의 상태를 이해 하려면 탑재 상태를 확인할 수 있습니다.

- 인수에 대 한 사용 탑재를 만들 때 **-탑재 경로** 는 기본적으로 탑재의 고유 식별자입니다. 다음 명령에서 동일한 문자열 (있는 경우 끝에 "/" 포함)를 사용 합니다.

- 탑재는 읽기 전용입니다. 모든 디렉터리 또는 탑재를 아래에 있는 파일을 만들 수 없습니다.

- 탑재 디렉터리 및 파일을 변경할 수 있는 권장 하지 않습니다. 탑재를 만든 후 모든 변경 내용이 나 업데이트 된 원격 위치에 반영 되지 않습니다의 HDFS에 탑재 합니다. 변경 내용을 원격 위치에서 발생 하는 경우 삭제 하 고 업데이트 된 상태를 반영 하도록 탑재 다시 선택할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
