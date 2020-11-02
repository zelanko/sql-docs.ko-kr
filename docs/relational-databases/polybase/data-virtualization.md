---
title: 외부 데이터 가상화
description: 이 페이지에서는 ODBC 데이터 원본에 대해 외부 테이블 만들기 마법사를 사용하는 단계를 자세히 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.metadata: seo-lt-2019
ms.openlocfilehash: 1cfc3dc5fa707a10f6adcf6e12122698ff4f9428
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92524020"
---
# <a name="use-the-external-table-wizard-with-odbc-data-sources"></a>ODBC 데이터 원본과 함께 외부 테이블 마법사 사용

SQL Server 2019의 주요 시나리오 중 하나는 데이터를 가상화하는 기능입니다. 이 프로세스를 통해 데이터를 원래 위치에 유지할 수 있습니다. SQL Server의 데이터를 *가상화* 하여 SQL Server의 다른 테이블처럼 쿼리할 수 있습니다. 이 프로세스는 ETL 프로세스의 필요성을 최소화합니다. 이 프로세스는 PolyBase 커넥터를 사용하여 수행할 수 있습니다. 데이터 가상화에 대한 자세한 내용은 [PolyBase 시작](polybase-guide.md)을 참조하세요.

다음 동영상에서는 데이터 가상화를 소개합니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-Data-Virtualization/player?WT.mc_id=dataexposed-c9-niner]


## <a name="start-the-external-table-wizard"></a>외부 테이블 마법사 시작

[**azdata cluster endpoints list**](../../big-data-cluster/deployment-guidance.md#endpoints) 명령을 사용하여 얻은 **sql-server-master** 엔드포인트의 IP 주소/포트 번호를 사용하여 마스터 인스턴스에 연결합니다. 개체 탐색기에서 **데이터베이스** 노드를 확장합니다. 그런 다음, 기존 SQL Server 인스턴스에서 데이터를 가상화할 데이터베이스 중 하나를 선택합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **외부 테이블 만들기** 를 선택하여 데이터 가상화 마법사를 시작합니다. 명령 팔레트에서 데이터 가상화 마법사를 시작할 수도 있습니다. Windows에서 Ctrl+Shift+P를 사용하거나 Mac에서 Cmd+Shift+P를 사용합니다.

![데이터 가상화 마법사](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>데이터 원본 선택

데이터베이스 중 하나에서 마법사를 시작하는 경우 대상 드롭다운 상자가 자동으로 채워집니다. 이 페이지에서는 대상 데이터베이스를 입력하거나 변경할 수 있는 옵션도 제공됩니다. 마법사에서 지원하는 외부 데이터 원본 유형은 SQL Server, Oracle, MongoDB 및 Teradata입니다.

> [!NOTE]
>SQL Server는 기본적으로 강조 표시됩니다.


![데이터 원본 선택](media/data-virtualization/select-data-source.png)

계속 진행하려면 **다음** 을 선택합니다.

## <a name="create-a-database-master-key"></a>데이터베이스 마스터 키 만들기

이 단계에서는 데이터베이스 마스터 키를 만듭니다. 마스터 키를 만들어야 합니다. 마스터 키는 외부 데이터 원본에 사용되는 자격 증명을 보호합니다. 마스터 키에 대해 강력한 암호를 선택합니다. 또한 **BACKUP MASTER KEY** 를 사용하여 마스터 키를 백업합니다. 안전한 오프 사이트 위치에 백업을 저장합니다.

![데이터베이스 마스터 키 만들기](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> 데이터베이스 마스터 키가 이미 있는 경우 이 단계는 자동으로 무시됩니다.

## <a name="enter-external-data-source-credentials"></a>외부 데이터 원본 자격 증명 입력

이 단계에서는 외부 데이터 원본 및 자격 증명 세부 정보를 입력하여 외부 데이터 원본 개체를 만듭니다. 자격 증명은 데이터베이스 개체가 데이터 원본에 연결하는 데 사용됩니다. 외부 데이터 원본의 이름을 입력합니다. 예를 들어 테스트입니다. 외부 데이터 원본 SQL Server 연결 세부 정보를 제공합니다. 외부 데이터 원본을 만들 **서버 이름** 및 **데이터베이스 이름** 을 입력합니다.

다음 단계는 자격 증명을 구성하는 것입니다. 자격 증명의 이름을 입력합니다. 이 이름은 사용자가 만든 외부 데이터 원본의 로그인 정보를 안전하게 저장하는 데 사용되는 데이터베이스 범위 자격 증명입니다. 예제는 `TestCred`입니다. 데이터 원본에 연결할 사용자 이름과 암호를 입력하세요.

![3단계 - 데이터 원본에 대한 연결 만들기 스크린샷](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>외부 데이터 테이블 매핑

다음 페이지에서 외부 보기를 만들 테이블을 선택합니다. 부모 데이터베이스를 선택하면 자식 테이블도 포함됩니다. 테이블을 선택하면 오른쪽에 매핑 테이블이 나타납니다. 여기서 형식을 변경할 수 있습니다. 선택한 외부 테이블 자체의 이름을 변경할 수도 있습니다.

![4단계 - 외부 테이블에 데이터 원본 개체 매핑 스크린샷](media/data-virtualization/data-table-map.png)

> [!NOTE]
>매핑 보기를 변경하려면 선택한 다른 테이블을 두 번 클릭합니다.

> [!IMPORTANT]
>외부 테이블 도구에서 사진 형식은 지원되지 않습니다. 사진 형식이 포함된 외부 보기를 만드는 경우 테이블이 생성된 후 오류가 표시됩니다. 하지만 테이블은 여전히 생성됩니다.

## <a name="summary"></a>요약

이 단계에서는 선택 항목의 요약을 보여줍니다. 데이터베이스 범위 자격 증명의 이름과 대상 데이터베이스에서 생성된 외부 데이터 원본 개체가 제공됩니다. 외부 데이터 원본을 생성하는 데 사용되는 구문을 T-SQL에서 스크립트 아웃하려면 **스크립트 생성** 을 선택합니다. **만들기** 를 선택하여 외부 데이터 원본 개체를 만듭니다.

![요약 화면](media/data-virtualization/virtualize-data-summary.png)

**만들기** 를 선택하면 대상 데이터베이스에서 생성된 외부 데이터 원본 개체가 표시됩니다.

![외부 데이터 원본](media/data-virtualization/external-data-sources.png)

**스크립트 생성** 을 선택하면 외부 데이터 원본 개체를 만들기 위해 생성된 T-SQL 쿼리가 표시됩니다.

![스크립트 생성](media/data-virtualization/generated-script.png)

> [!NOTE]
> **스크립트 생성** 은 마법사의 마지막 페이지에만 표시되어야 합니다. 현재 모든 페이지에 표시됩니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터 및 관련 시나리오에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.
