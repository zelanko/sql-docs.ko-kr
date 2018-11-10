---
title: Curl을 사용 하 여 SQL Server 2019 CTP 2.1에서 HDFS에 데이터 로드 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: a5f580ab39ef7338f424975d9667745131ee748f
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221629"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-ctp-21"></a>Curl을 사용 하 여 SQL Server 2019 CTP 2.1에서 HDFS에 데이터를 로드

이 문서를 사용 하는 방법에 설명 **curl** SQL Server 2019 CTP 2.1에서 HDFS에 데이터를 로드 합니다.

## <a name="obtain-the-service-external-ip"></a>서비스 외부 IP 가져오기

WebHDFS는 배포가 완료 되 고 액세스 Knox를 통과 하는 경우 시작 됩니다. Knox 끝점 Kubernetes 서비스를 통해 노출 됩니다 (지금은) 호출 **lb-보안-서비스**합니다.  해야 하는 파일 업로드/다운로드 하는 데 CURL을 사용 해야 하는 WebHDFS URL을 만드는 데는 **lb-보안-서비스** 서비스 외부 IP 주소 및 클러스터의 이름입니다. 이 명령을 실행 하 여 서비스-보안-lb 서비스 외부 IP 주소를 가져올 수 있습니다.

```bash
kubectl get service service-security-lb -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> 합니다 `<cluster name>` 같습니다. mssqlctl 실행 했을 때 제공한 클러스터의 이름에 클러스터 만들기 `<cluster name>`합니다.

## <a name="construct-the-url-to-access-webhdfs"></a>WebHDFS를 액세스 하는 URL 생성

이제는 WebHDFS를 다음과 같이 액세스 하기 위한 URL을 생성할 수 있습니다.

`https://<service-security-lb service external IP address>:30433/gateway/default/webhdfs/v1/`

이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>파일 목록

아래 목록 파일을 **hdfs: / / / airlinedata** 다음 curl 명령을 사용 합니다.

```bash
curl -i -k -u root:root-password -X GET 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>HDFS에 로컬 파일을 저장 합니다.

새 파일을 저장할 **test.csv** airlinedata 디렉터리로 로컬 디렉터리에서 (**Content-type** 매개 변수는 필수) 다음 curl 명령을 사용 합니다.

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>디렉터리 만들기

디렉터리를 만들려면 **테스트** 아래에서 `hdfs:///` 다음 명령을 사용 합니다.

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [빅 데이터 클러스터 SQL Server 란?](big-data-cluster-overview.md)합니다.