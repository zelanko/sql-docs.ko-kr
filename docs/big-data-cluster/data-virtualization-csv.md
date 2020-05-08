---
title: 스토리지 풀에서 CSV 데이터 가상화
subtitle: SQL Server 빅 데이터 클러스터
description: 빅 데이터 클러스터에서 CSV 파일의 가상화를 위해 외부 테이블을 만드는 방법
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/24/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.metadata: seo-lt-2019
ms.openlocfilehash: 6981eea5cb4d327303755adc74d5610637eb70b0
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588259"
---
# <a name="virtualize-csv-data-from-storage-pool-big-data-clusters"></a>스토리지 풀에서 CSV 데이터 가상화(빅 데이터 클러스터)

SQL Server 빅 데이터 클러스터는 HDFS에서 CSV 파일로부터 데이터를 가상화할 수 있습니다. 이 프로세스를 사용하면 데이터가 원래 위치에 유지되면서도 다른 테이블처럼 SQL Server 인스턴스에서 쿼리될 수 있습니다. 이 기능은 PolyBase 커넥터를 사용하며, ETL 프로세스의 필요성을 최소화합니다. 데이터 가상화에 대한 자세한 내용은 [PolyBase란?](../relational-databases/polybase/polybase-guide.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- [배포된 빅 데이터 클러스터](deployment-guidance.md)
- [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)

## <a name="select-or-upload-a-csv-file-for-data-virtualization"></a>데이터 가상화에 사용할 CSV 파일 선택 또는 업로드 

ADS(Azure Data Studio)에서 빅 데이터 클러스터의 [SQL Server 마스터 인스턴스에 연결](connect-to-big-data-cluster.md#master)합니다. 연결되면 개체 탐색기에서 HDFS 요소를 확장하여 데이터를 가상화할 CSV 파일을 찾습니다. 

이 자습서에서는 **Data**라는 이름의 새 디렉터리를 만들겠습니다.

1. HDFS 루트 디렉터리 바로 가기 메뉴를 마우스 오른쪽 단추로 클릭합니다.
2. **새 디렉터리**를 클릭합니다.
3. 새 디렉터리의 이름을 *Data*라고 지정합니다.

샘플 데이터를 업로드합니다. 간단하게 살펴볼 수 있도록 샘플 csv 데이터 파일을 사용해도 됩니다. 이 문서에서는 [미국운수부](https://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp?pn=1)의 항공편 지연 원인 데이터를 사용합니다. 원시 데이터를 다운로드하고 컴퓨터로 데이터를 추출합니다. 파일의 이름을 *airline_delay_causes.csv*로 지정합니다.

추출한 샘플 파일을 업로드하려면:

1. Azure Data Studio에서, 앞에서 만든 새 디렉터리를 마우스 오른쪽 단추로 클릭합니다.  
2. **파일 업로드**를 클릭합니다.

![HDFS의 예제 csv 파일](media/data-virtualization/100-csv-sample-file-hdfs.png)

Azure Data Studio가 빅 데이터 클러스터의 HDFS로 파일을 업로드합니다.

## <a name="create-the-storage-pool-external-data-source-in-your-target-database"></a>대상 데이터베이스에서 스토리지 풀 외부 데이터 원본을 만듭니다.

스토리지 풀 외부 데이터 원본은 빅 데이터 클러스터의 데이터베이스에 기본적으로 생성되지 않습니다. 외부 테이블을 만들기 전에 다음 Transact-SQL 쿼리를 사용하여 대상 데이터베이스에 기본 **SqlStoragePool** 외부 데이터 원본을 만듭니다. 먼저 쿼리의 컨텍스트를 대상 데이터베이스로 변경해야 합니다.

```sql
-- Create the default storage pool source for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="create-the-external-table"></a>외부 테이블 만들기

ADS에서 CSV 파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **CSV 파일에서 외부 테이블 만들기**를 선택합니다. 디렉터리 아래의 파일이 동일한 스키마를 따르는 경우 HDFS의 디렉터리에서 CSV 파일로 외부 테이블을 만들 수도 있습니다. 이렇게 하면 개별 파일을 처리하고 결합된 데이터에 대해 조인된 결과 집합을 가져올 필요 없이 디렉터리 수준에서 데이터를 가상화할 수 있습니다. Azure Data Studio에서 외부 테이블을 만드는 단계를 안내합니다.

데이터베이스, 데이터 원본, 테이블 이름, 스키마, 테이블의 외부 파일 형식 이름을 지정합니다.

**다음**을 클릭합니다.

## <a name="preview-data"></a>데이터 미리 보기

Azure Data Studio에서 가져온 데이터의 미리 보기를 제공합니다.

![외부 데이터 원본 자격 증명](media/data-virtualization/130-csv-preview-data.png)

미리 보기를 확인한 후에는 **다음**을 클릭하여 계속 진행합니다.

## <a name="modify-columns"></a>열 수정

다음 창에서 만들려는 외부 테이블의 열을 수정할 수 있습니다. 열 이름을 변경하고, 데이터 형식을 변경하고, Nullable 행을 허용할 수 있습니다. 

![외부 데이터 원본 자격 증명](media/data-virtualization/140-csv-modify-columns.png)

대상 열을 확인한 후에 **다음**을 클릭합니다.

## <a name="summary"></a>요약

이 단계에서는 선택 옵션을 요약해서 설명합니다. SQL Server 이름, 데이터베이스 이름, 테이블 이름, 테이블 스키마, 외부 테이블 정보가 제공됩니다. 이 단계에서 스크립트를 생성하거나 테이블을 만들 수 있습니다. **스크립트 생성**은 T-SQL에서 외부 데이터 원본을 만들기 위한 스크립트를 만듭니다. **테이블 만들기**는 외부 데이터 원본을 만듭니다.

![요약 화면](media/data-virtualization/150-csv-virtualize-data-summary.png)

**테이블 만들기**를 클릭하면 SQL Server가 대상 데이터베이스에 외부 테이블을 만듭니다.

**스크립트 생성**을 클릭하면 Azure Data Studio가 외부 테이블을 만들기 위한 T-SQL 쿼리를 만듭니다.

테이블을 만든 후에는 SQL Server 인스턴스에서 직접 T-SQL을 사용하여 쿼리할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터 및 관련 시나리오에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](big-data-cluster-overview.md)을 참조하세요.
