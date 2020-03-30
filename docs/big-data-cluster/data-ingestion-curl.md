---
title: curl을 사용하여 HDFS로 데이터 로드 | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: curl을 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 HDFS에 데이터를 로드합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 970c4f51535395a940a9c47e77d864d00c1f403c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73706630"
---
# <a name="use-curl-to-load-data-into-hdfs-on-big-data-clusters-2019"></a>curl을 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 HDFS에 데이터 로드

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 **curl**을 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 HDFS로 데이터를 로드하는 방법을 설명합니다.

## <a name="prerequisites"></a><a id="prereqs"></a> 필수 조건

- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="obtain-the-service-external-ip"></a>서비스 외부 IP 가져오기

배포가 완료되면 WebHDFS가 시작되고 해당 액세스가 Knox를 통과합니다. Knox 엔드포인트는 **gateway-svc-external**이라는 Kubernetes 서비스를 통해 공개됩니다.  파일을 업로드/다운로드하는 데 필요한 WebHDFS URL을 만들려면 **gateway-svc-external** 서비스 외부 IP 주소와 빅 데이터 클러스터의 이름이 필요합니다. 다음 명령을 실행하여 **gateway-svc-external** 서비스 외부 IP 주소를 가져올 수 있습니다.

```bash
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> 여기서 `<big data cluster name>`은 배포 구성 파일에서 지정한 클러스터의 이름입니다. 기본 이름은 `mssql-cluster`입니다.

## <a name="construct-the-url-to-access-webhdfs"></a>WebHDFS에 액세스하는 데 사용할 URL 생성

이제 다음과 같이 WebHDFS에 액세스하는 데 사용할 URL을 생성할 수 있습니다.

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

다음은 그 예입니다.

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>파일 나열

**hdfs:///product_review_data** 아래에 있는 파일을 나열하려면 다음 curl 명령을 사용합니다.

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>HDFS에 로컬 파일 저장

로컬 디렉터리의 새 파일 **test.csv**를 product_review_data 디렉터리에 저장하려면 다음 curl 명령을 사용합니다(**Content-Type** 매개 변수가 필요함).

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>디렉터리 만들기

**아래에**test`hdfs:///` 디렉터리를 만들려면 다음 명령을 사용합니다.

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](big-data-cluster-overview.md)을 참조하세요.
