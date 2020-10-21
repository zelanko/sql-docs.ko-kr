---
title: curl을 사용하여 HDFS로 데이터 로드 | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: curl을 사용하여 SQL Server 2019 빅 데이터 클러스터의 HDFS에 데이터를 로드합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ae893bb1e291b244b5101ccfb2ed66bcf765f049
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866848"
---
# <a name="use-curl-to-load-data-into-hdfs-on-big-data-clusters-2019"></a>curl을 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 HDFS에 데이터 로드

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 **curl**을 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 HDFS로 데이터를 로드하는 방법을 설명합니다.

## <a name="prerequisites"></a><a id="prereqs"></a> 필수 조건

- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="obtain-the-service-external-ip"></a>서비스 외부 IP 가져오기

배포가 완료되면 WebHDFS가 시작되고 해당 액세스가 Knox를 통과합니다. Knox 엔드포인트는 **gateway-svc-external**이라는 Kubernetes 서비스를 통해 공개됩니다.  파일을 업로드/다운로드하는 데 필요한 WebHDFS URL을 만들려면 **gateway-svc-external** 서비스 외부 IP 주소와 빅 데이터 클러스터의 이름이 필요합니다. 다음 명령을 실행하여 **gateway-svc-external** 서비스 외부 IP 주소를 가져올 수 있습니다.

```terminal
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> 여기서 `<big data cluster name>`은 배포 구성 파일에서 지정한 클러스터의 이름입니다. 기본 이름은 `mssql-cluster`입니다.

## <a name="construct-the-url-to-access-webhdfs"></a>WebHDFS에 액세스하는 데 사용할 URL 생성

이제 다음과 같이 WebHDFS에 액세스하는 데 사용할 URL을 생성할 수 있습니다.

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

다음은 그 예입니다.

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="authentication-with-active-directory"></a>Active Directory를 사용한 인증

Active Directory를 사용한 배포의 경우 `curl` 및 Negotiate 인증과 함께 인증 매개 변수를 사용합니다. 

Active Directory 인증과 함께 `curl`을 사용하려면 다음 명령을 실행합니다.

```
kinit <username>
```

이 명령은 `curl`에서 사용할 Kerberos 토큰을 생성합니다. 다음 섹션에서 설명하는 명령은 `curl`에 대해 `--anyauth` 매개 변수를 지정합니다. Negotiate 인증이 필요한 URL의 경우 `curl`이 생성된 Kerberos 토큰을 자동으로 검색하고 사용자 이름과 암호 대신 사용하여 URL에 인증합니다.

## <a name="list-a-file"></a>파일 나열

**hdfs:///product_review_data** 아래에 있는 파일을 나열하려면 다음 curl 명령을 사용합니다.

```terminal
curl -i -k --anyauth -u root:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

루트를 사용하지 않는 엔드포인트의 경우 다음 curl 명령을 사용합니다.

```terminal
curl -i -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>HDFS에 로컬 파일 저장

로컬 디렉터리의 새 파일 **test.csv**를 product_review_data 디렉터리에 저장하려면 다음 curl 명령을 사용합니다(**Content-Type** 매개 변수가 필요함).

```terminal
curl -i -L -k --anyauth -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

루트를 사용하지 않는 엔드포인트의 경우 다음 curl 명령을 사용합니다.

```terminal
curl -i -L -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>디렉터리 만들기

`hdfs:///` 아래에 **test** 디렉터리를 만들려면 다음 명령을 사용합니다.

```terminal
curl -i -L -k --anyauth -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]
루트를 사용하지 않는 엔드포인트의 경우 다음 curl 명령을 사용합니다.

```terminal
curl -i -L -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](big-data-cluster-overview.md)을 참조하세요.
