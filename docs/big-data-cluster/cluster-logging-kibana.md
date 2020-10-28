---
title: Kibana 대시보드를 사용하여 클러스터 로그 확인
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 Kibana 대시보드를 사용하여 클러스터를 모니터링합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 10/01/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 66b405f020728c0ed7040a712d56bcadc3180e38
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378475"
---
# <a name="check-out-cluster-logs--with-kibana-dashboard"></a>Kibana 대시보드를 사용하여 클러스터 로그 확인

이 문서에서는 SQL Server 빅 데이터 클러스터 내에서 애플리케이션을 모니터링하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server 2019 빅 데이터 클러스터](deployment-guidance.md)
- [azdata 명령줄 유틸리티](deploy-install-azdata.md)

## <a name="capabilities"></a>기능

SQL Server 2019에서 애플리케이션을 만들고, 삭제, 설명, 초기화, 나열, 실행 및 업데이트할 수 있습니다. 다음 표에서는 **azdata** 와 함께 사용할 수 있는 애플리케이션 배포 명령을 설명합니다.

|명령 |설명 |
|:---|:---|
|`azdata bdc endpoint list` | 빅 데이터 클러스터의 엔드포인트를 나열합니다. |


다음 예제를 사용하여 **Kibana 대시보드** 의 엔드포인트를 나열할 수 있습니다.

```bash
azdata bdc endpoint list --endpoint-name logsui 
```

출력에서는 클러스터 사용자 이름 및 암호를 사용하여 로그인할 수 있는 엔드포인트를 제공합니다. 

![Kibana 대시보드](media/big-data-cluster-monitor-cluster/kibana-dashboard-endpoint.png)


Kibana 대시보드로 연결되는 링크:

![Kibana 대시보드](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> (기존) Microsoft Edge 브라우저는 Kibana와 호환되지 않으므로 대시보드를 올바르게 표시하려면 Chromium 기반 브라우저를 사용해야 합니다. 지원되지 않는 브라우저를 사용하여 대시보드를 로드하면 빈 페이지가 표시됩니다. Kibana의 지원되는 브라우저를 보려면 여기를 참조하세요.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
