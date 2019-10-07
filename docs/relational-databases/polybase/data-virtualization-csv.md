---
title: SQL Server 2019 CTP 2.0에서 외부 데이터 가상화 | Microsoft Docs
description: 이 페이지에서는 CSV 파일에 대해 외부 테이블 만들기 마법사를 사용하는 단계를 자세히 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6a8ce50e4e359c8ce8dc2b0015300f9a7afb88d1
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710603"
---
# <a name="use-the-external-table-wizard-with-csv-files"></a>CSV 파일과 함께 외부 테이블 마법사 사용

또한 SQL Server 2019를 사용하면 HDFS의 CSV 파일에서 데이터를 가상화할 수 있습니다.  이 프로세스는 데이터가 원래 위치를 유지하도록 하지만 SQL Server의 다른 테이블처럼 쿼리될 수 있게 SQL Server 인스턴스에서 데이터를 **가상화**할 수 있습니다. 이 기능은 ETL 프로세스의 필요성을 최소화합니다. 이러한 효과는 Polybase 커넥터를 사용하여 얻을 수 있습니다. 데이터 가상화에 대한 자세한 내용은 [PolyBase 시작](polybase-guide.md) 문서를 참조하세요.

## <a name="prerequisite"></a>사전 요구 사항

CTP 2.4부터 데이터 풀 및 스토리지 풀 외부 데이터 원본은 더 이상 빅 데이터 클러스터에 기본적으로 생성되지 않습니다. 마법사를 사용하기 전에 다음 Transact-SQL 쿼리를 사용하여 대상 데이터베이스에 기본 **SqlStoragePool** 외부 데이터 원본을 만듭니다. 먼저 쿼리의 컨텍스트를 대상 데이터베이스로 변경해야 합니다.

```sql
-- Create default data sources for SQL Big Data Cluster
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
    CREATE EXTERNAL DATA SOURCE SqlDataPool
    WITH (LOCATION = 'sqldatapool://controller-svc/default');

IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://controller-svc/default');
```

## <a name="launch-the-external-table-wizard"></a>외부 테이블 마법사 시작

IP 주소를 사용하여 HDFS 루트에 연결합니다. 개체 탐색기에서 요소를 확장합니다. 그런 다음, 기존 SQL Server 인스턴스로 데이터를 가상화할 CSV 중 하나를 선택합니다. 파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **CSV 파일에서 외부 테이블 만들기**를 선택합니다. 폴더 아래의 파일이 동일한 스키마를 따르는 경우 HDFS의 폴더에서 CSV 파일로 외부 테이블을 만들 수도 있습니다. 이렇게 하면 개별 파일을 처리하고 결합된 데이터에 대해 조인된 결과 집합을 가져올 필요 없이 폴더 수준에서 데이터를 가상화할 수 있습니다. 그러면 데이터 가상화 마법사가 시작됩니다. 또한 Ctrl+Shift+P(Windows) 및 Cmd+Shift+P(Mac)를 입력하여 명령 팔레트에서 데이터 가상화 마법사를 시작할 수도 있습니다.

![데이터 가상화 마법사](media/data-virtualization/csv-virtualize-data-wizard.png)

## <a name="connect-to-a-sql-server-master-instance"></a>SQL Server 마스터 인스턴스에 연결

여기서 IP, 포트 및 자격 증명 정보를 사용하여 연결할 SQL 마스터 인스턴스를 지정할 수 있습니다. 이전에 저장된 연결은 **활성 SQL Server 연결** 드롭다운 상자를 통해 액세스할 수 있습니다. 
> [!NOTE]
>저장된 연결을 사용하는 경우 다른 필드는 차단됩니다.


![데이터 원본 선택](media/data-virtualization/csv-connect-to-master.png)

데이터베이스 마스터 키를 설정하는 마법사의 다음 단계를 계속 진행하려면 다음을 클릭합니다.

## <a name="select-destination-database"></a>대상 데이터베이스 선택

이 단계에서는 데이터를 가상화할 대상 데이터베이스를 선택합니다. 드롭다운 필드에는 이전 화면에서 지정된 SQL Master 인스턴스에 허용 가능한 모든 데이터베이스가 포함됩니다. 여기서 새 외부 테이블의 이름을 지정하고 사용할 스키마를 볼 수도 있습니다.

![데이터베이스 마스터 키 만들기](media/data-virtualization/csv-select-destination.png)


## <a name="preview-data"></a>데이터 미리 보기

이 창에서 유효성 검사를 위해 CSV 파일의 처음 50개 행의 미리 보기를 볼 수 있습니다.

미리 보기를 확인한 후에는 "다음"을 클릭하여 계속 진행합니다.

![외부 데이터 원본 자격 증명](media/data-virtualization/csv-preview-data.png)

## <a name="modify-columns"></a>열 수정

다음 창에서 만들려는 외부 테이블의 열을 수정할 수 있습니다. 열 이름을 변경하고, 데이터 형식을 변경하고, Nullable 행을 허용할 수 있습니다. 

![외부 데이터 원본 자격 증명](media/data-virtualization/csv-modify-columns.png)


## <a name="summary"></a>요약

이 단계에서는 선택 옵션을 요약해서 설명합니다. SQL Master 인스턴스 및 제안된 외부 테이블 정보를 제공합니다. 이 단계에서는 T-SQL에서 외부 데이터 원본을 만드는 구문을 스크립팅하는 **"스크립트 생성"** 또는 외부 데이터 원본 개체를 만드는 **만들기** 옵션이 제공됩니다.

![요약 화면](media/data-virtualization/csv-virtualize-data-summary.png)

"만들기"를 클릭하면 대상 데이터베이스에서 생성된 외부 테이블을 볼 수 있습니다.

![외부 데이터 원본](media/data-virtualization/csv-external-data-sources.png)

**스크립트 생성**을 클릭하면 외부 데이터 원본 개체를 만들기 위한 T-SQL 쿼리가 생성되는 것을 볼 수 있습니다.

![스크립트 생성](media/data-virtualization/csv-generated-script.png)

> [!NOTE]
> 스크립트 생성은 마법사의 마지막 페이지에만 표시됩니다. 현재 모든 페이지에 표시됩니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터 및 관련 시나리오에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.
