---
title: Curl을 사용 하 여 HDFS에서 데이터 로드 | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터에서 HDFS에 데이터를 로드 하는 데 curl을 사용 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 74e08c16e528c580bf78b3928a1aaf0c9b3eb069
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472097"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터에서 HDFS에 데이터를 로드 하는 데 curl을 사용

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서를 사용 하는 방법에 설명 **curl** SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 HDFS에 데이터를 로드할 수 있습니다.

## <a name="obtain-the-service-external-ip"></a>서비스 외부 IP 가져오기

WebHDFS는 배포가 완료 되 고 액세스 Knox를 통과 하는 경우 시작 됩니다. Knox 끝점을 호출 하는 Kubernetes 서비스를 통해 노출 되 **게이트웨이 svc 외부**합니다.  필요한 파일을 업로드/다운로드 하는 데 필요한 WebHDFS URL을 만들려면 합니다 **게이트웨이 svc 외부** 서비스 외부 IP 주소 및 클러스터의 이름입니다. 가져올 수 있습니다 합니다 **게이트웨이 svc 외부** 다음 명령을 실행 하 여 외부 IP 주소를 서비스 합니다.

```bash
kubectl get service gateway-svc-external -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> 합니다 `<cluster name>` 실행 했을 때 제공한 클러스터의 이름은 여기에 `mssqlctl cluster create --name <cluster name>`입니다.

## <a name="construct-the-url-to-access-webhdfs"></a>WebHDFS를 액세스 하는 URL 생성

이제는 WebHDFS를 다음과 같이 액세스 하기 위한 URL을 생성할 수 있습니다.

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>파일 목록

목록 파일에 **hdfs: / / / airlinedata**, 다음 curl 명령을 사용 합니다.

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>HDFS에 로컬 파일을 저장 합니다.

새 파일을 저장할 **test.csv** airlinedata 디렉터리로 로컬 디렉터리에서 다음 curl 명령을 사용 하 여 (합니다 **Content-type** 매개 변수는 필수):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>디렉터리 만들기

디렉터리를 만들려면 **테스트할** 아래에서 `hdfs:///`, 다음 명령을 사용 하 여:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [빅 데이터 클러스터 SQL Server 란?](big-data-cluster-overview.md)합니다.
