---
title: Active Directory 모드로 연결
titleSuffix: SQL Server Big Data Cluster
description: Active Directory 도메인의 SQL Server 빅 데이터 클러스터에 연결하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 547337ea7573429bcccc1eb9b9c36914f286a2a5
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257310"
---
# <a name="connect-big-data-clusters-2019-active-directory-mode"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 연결: Active Directory 모드

이 문서에서는 Active Directory 모드로 배포된 SQL Server 빅 데이터 클러스터 엔드포인트에 연결하는 방법을 설명합니다. 이 문서의 작업을 수행하려면 SQL Server 빅 데이터 클러스터가 Active Directory 모드로 배포되어 있어야 합니다. 클러스터가 없는 경우 [Active Directory 모드로 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deploy.md)를 참조하세요.

## <a name="overview"></a>개요

AD 인증을 사용하여 SQL Server 마스터 인스턴스에 로그인합니다.

SQL Server 인스턴스에 대한 AD 연결을 확인하려면 `sqlcmd`를 사용하여 SQL 마스터 인스턴스에 연결합니다. 배포 시 제공된 그룹(`clusterUsers` 및 `clusterAdmins`)에 대한 로그인이 자동으로 만들어집니다.

Linux를 사용하는 경우 먼저 `kinit`를 AD 사용자 권한으로 실행한 다음, `sqlcmd`를 실행합니다. Windows를 사용하는 경우 **도메인 조인 클라이언트 머신**에서 원하는 사용자 권한으로 로그인하면 됩니다.

## <a name="connect-to-master-instance-from-linuxmac"></a>Linux/Mac에서 마스터 인스턴스에 연결

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

## <a name="connect-to-master-instance-from-windows"></a>Windows에서 마스터 인스턴스에 연결

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

## <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>Azure Data Studio 또는 SSMS를 사용하여 SQL Server 마스터 인스턴스에 로그인

도메인 조인 클라이언트에서 SSMS 또는 Azure Data Studio를 열어 마스터 인스턴스에 연결할 수 있습니다. 이는 AD 인증을 사용하여 SQL Server 인스턴스에 연결하는 것과 동일한 환경입니다.

SSMS에서:

![SSMS에서 SQL Server에 연결 대화 상자](./media/deploy-active-directory/image23.png)

Azure Data Studio에서:

![Azure Data Studio에서 SQL Server에 연결 대화 상자](./media/deploy-active-directory/image24.png)}

## <a name="log-in-to-controller-with-ad-authentication"></a>AD 인증을 사용하여 컨트롤러에 로그인

### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>Linux/Mac에서 AD 인증을 사용하여 컨트롤러에 연결

[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 및 AD 인증을 사용하여 컨트롤러 엔드포인트에 연결하는 두 가지 옵션이 있습니다. *--endpoint/-e* 매개 변수를 사용할 수 있습니다.

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

또는 빅 데이터 클러스터 이름인 *--namespace/-n* 매개 변수를 사용하여 연결할 수 있습니다.

```bash
kinit <username>@<domain name>
azdata login -n <clusterName> --auth ad
```

### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>Windows에서 AD 인증을 사용하여 컨트롤러에 연결

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

## <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>Knox 게이트웨이에 AD 인증 사용(webHDFS)

Knox 게이트웨이 엔드포인트를 통해 curl을 사용하여 HDFS 명령을 실행할 수도 있습니다. 이 경우 Knox에 대한 AD 인증이 필요합니다. 아래 curl 명령은 Knox 게이트웨이를 통해 webHDFS REST 호출을 실행하여 `products`라는 디렉터리를 만듭니다.

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="next-steps"></a>다음 단계

[SQL Server 빅 데이터 클러스터 Active Directory 통합 문제 해결](troubleshoot-active-directory.md)

[개념: Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deployment-background.md)
