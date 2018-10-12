---
title: SQL Server 2019 CTP 2.0에서 외부 데이터 가상화 | Microsoft Docs
description: ''
author: Abiola
ms.author: aboke
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: dfd4460c51e4aeef8e9faff8479e7edf2678c35f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627321"
---
# <a name="use-the-data-external-table-wizard-with-external-tables"></a>외부 테이블에 데이터 외부 테이블 마법사 사용

SQL Server 2019 CTP 2.0의 주요 시나리오 중 하나는 데이터를 가상화하는 기능입니다.  이 프로세스는 데이터가 원래 위치를 유지하도록 하지만 SQL Server의 다른 테이블처럼 쿼리될 수 있게 SQL Server 인스턴스에서 데이터를 **가상화**할 수 있습니다. 이렇게 하면 ETL 프로세스의 필요성이 최소화됩니다. 이러한 효과는 Polybase 커넥터를 사용하여 얻을 수 있습니다. 데이터 가상화에 대한 자세한 내용은 [PolyBase 시작](polybase-guide.md) 문서를 참조하세요.

## <a name="launch-the-external-table-wizard"></a>외부 테이블 마법사 시작

배포 스크립트의 끝에서 가져온 IP 주소/포트 번호(31433)를 사용하여 마스터 인스턴스에 연결합니다. 개체 탐색기에서 **데이터베이스** 노드를 확장합니다. 그런 후 기존 SQL Server 인스턴스에서 데이터를 가상화하려는 데이터베이스 중 하나를 선택합니다. 해당 데이터베이스를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **외부 테이블 만들기**를 선택합니다. 그러면 데이터 가상화 마법사가 시작됩니다. 또한 Ctrl+Shift+P(Windows) 및 Cmd+Shift+P(Mac)를 입력하여 명령 팔레트에서 데이터 가상화 마법사를 시작할 수도 있습니다.

![데이터 가상화 마법사](media/data-virtualization/virtualize-data-wizard.png)
## <a name="select-a-data-source"></a>데이터 원본 선택

데이터베이스 중 하나에서 마법사를 시작한 경우 대상 드롭다운이 자동으로 채워지는 것을 볼 수 있습니다. 이 화면에서 대상 데이터베이스를 입력하거나 변경하기 위한 옵션도 제공됩니다. 마법사에서 지원하는 외부 데이터 원본 유형은 SQL Server 및 Oracle입니다.

> [!NOTE]
>SQL Server는 기본적으로 강조 표시됨


![데이터 원본 선택](media/data-virtualization/select-data-source.png)

데이터베이스 마스터 키를 설정하는 마법사의 다음 단계를 계속 진행하려면 다음을 클릭합니다.

## <a name="create-database-master-key"></a>데이터베이스 마스터 키 만들기

이 단계에서는 데이터베이스 마스터 키를 만들라는 메시지가 표시됩니다. 마스터 키는 외부 데이터 원본에 사용되는 자격 증명을 보호하므로 반드시 만들어야 합니다. 마스터 키에 대해 강력한 암호를 선택합니다. 또한 마스터 키는 BACKUP MASTER KEY를 사용하여 백업하고 백업 복사본을 외부의 안전한 위치에 보관해야 합니다.

![데이터베이스 마스터 키 만들기](media/data-virtualization/virtualize-data-master-key.png)

> [!IMPORTANT]
> 데이터베이스 마스터 키가 이미 있는 경우 입력 필드가 제한되며 이 단계를 무시할 수 있습니다. “다음”을 클릭하여 마법사의 다음 페이지로 간단히 이동할 수 있습니다.

> [!NOTE]
> 강력한 암호를 선택하지 않으면 마법사의 마지막 단계가 됩니다. 이것은 알려진 문제로, 향후 릴리스에서 좀 더 이해하기 쉽게 수정될 예정입니다.

## <a name="enter-the-external-data-source-credentials"></a>외부 데이터 원본 자격 증명 입력

이 단계에서는 외부 데이터 원본 및 자격 증명 정보를 입력합니다. 이 단계에서는 외부 데이터 원본 개체를 만들고 데이터베이스 개체의 자격 증명을 사용하여 데이터 원본에 연결합니다. 외부 데이터 원본의 이름(예: Test)을 입력하고 외부 데이터 원본 SQL Server 연결 세부 정보 - 서버 이름과 해당 서버에서 외부 데이터 원본을 만들 데이터베이스 이름을 제공합니다.

다음 단계는 자격 증명을 구성하는 단계입니다. 따라서 만들려는 외부 데이터 원본의 로그인 정보를 안전하게 저장하고 데이터 원본에 연결하기 위한 사용자 이름과 암호를 제공하는 데 사용하는 데이터베이스 범위 자격 증명(예: TestCred)의 이름인 자격 증명 이름을 제공합니다.

![외부 데이터 원본 자격 증명](media/data-virtualization/data-source-credentials.png)

## <a name="external-data-table-mapping"></a>외부 데이터 테이블 매핑

다음 창에서 외부 뷰를 만들려는 테이블을 선택할 수 있습니다. 부모 데이터베이스를 선택하면 모든 하위 테이블도 포함됩니다. 테이블을 선택하면 오른쪽에 매핑 테이블이 표시될 수 있습니다. 여기서 ‘type’을 변경하고 선택한 외부 테이블 자체의 이름을 변경할 수 있습니다.

![외부 데이터 원본 자격 증명](media/data-virtualization/data-table-mapping.png)

> [!NOTE]
>선택한 다른 테이블을 두 번 클릭하면 매핑 뷰가 변경됩니다.

> [!IMPORTANT]
>외부 테이블 도구에서 사진 형식은 아직 지원되지 않습니다. 사진 형식으로 외부 뷰를 만들면 테이블이 생성된 후에 오류가 throw됩니다. 그렇지만 테이블은 계속 생성됩니다.

## <a name="summary"></a>요약

이 단계에서는 선택 옵션을 요약해서 설명합니다. 데이터베이스 범위 자격 증명의 이름과 대상 데이터베이스에서 생성될 외부 데이터 원본 개체가 표시됩니다. 이 단계에서는 T-SQL에서 외부 데이터 원본을 만드는 구문을 스크립팅하는 **"스크립트 생성"** 또는 외부 데이터 원본 개체를 만드는 **만들기** 옵션이 제공됩니다.

![요약 화면](media/data-virtualization/virtualize-data-summary.png)

“만들기”를 클릭하면 대상 데이터베이스에서 생성된 외부 데이터 원본 개체를 볼 수 있습니다.

![외부 데이터 원본](media/data-virtualization/external-data-sources.png)

**스크립트 생성**을 클릭하면 외부 데이터 원본 개체를 만들기 위한 T-SQL 쿼리가 생성되는 것을 볼 수 있습니다.

![스크립트 생성](media/data-virtualization/generated-script.png)

> [!NOTE]
> 스크립트 생성은 마법사의 마지막 페이지에만 표시됩니다. 현재 모든 페이지에 표시됩니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터 및 관련 시나리오에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터란?](../../big-data-cluster/big-data-cluster-overview.md)을 참조하세요.
