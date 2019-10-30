---
title: curl을 사용하여 HDFS로 데이터 로드 | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: '[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 HDFS에 데이터를 로드 하려면 말아 넘기기를 사용 합니다.'
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c65ce7fb6752240f0dd23a6dab195539146e7933
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049884"
---
# <a name="use-curl-to-load-data-into-hdfs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>말아 넘기기를 사용 하 여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에서 HDFS로 데이터 로드

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (미리 보기)에서 **말아 넘기기** 를 사용 하 여 HDFS로 데이터를 로드 하는 방법을 설명 합니다.

## <a id="prereqs"></a> 사전 요구 사항

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

예를 들어

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>파일 나열

**Hdfs:///product_review_data**아래에 있는 파일을 나열 하려면 다음의 말아 명령을 사용 합니다.

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>HDFS에 로컬 파일 저장

로컬 디렉터리에서 product_review_data 디렉터리에 새 파일을 저장 하려면 다음 말아 명령을 **사용 합니다 (** **content-type** 매개 변수가 필요 함).

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>디렉터리 만들기

`hdfs:///` 아래에 **test** 디렉터리를 만들려면 다음 명령을 사용합니다.

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](big-data-cluster-overview.md)을 참조하세요.
