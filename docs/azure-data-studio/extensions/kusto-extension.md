---
title: Azure Data Studio용 Kusto(KQL) 확장
description: 이 문서에서는 Azure Data Studio를 사용하여 Azure Data Explorer 클러스터에 연결하고 쿼리하는 방법을 설명합니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 52f8bb103aad960750a74be1a4e35b0d1d5be5d7
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364070"
---
# <a name="kusto-kql-extension-for-azure-data-studio-preview"></a>Azure Data Studio용 Kusto(KQL) 확장(미리 보기)

[Azure Data Studio](../what-is.md)용 Kusto(KQL) 확장을 사용하면 [Azure Data Explorer](https://docs.microsoft.com/azure/data-explorer/data-explorer-overview) 클러스터에 연결하고 쿼리할 수 있습니다.

이제 사용자가 Azure Data Explorer 클러스터에 연결하여 찾아보고, KQL 쿼리를 작성하여 실행하고, Kusto 커널 및 IntelliSense를 사용하여 Notebook을 작성할 수 있습니다. Azure Data Studio에서 네이티브 Kusto(KQL) 환경을 사용하도록 설정하면 데이터 엔지니어, 데이터 과학자, 데이터 분석가가 Azure Data Explorer에 저장된 방대한 데이터에서 추세와 변칙을 빠르게 관찰할 수 있습니다.

이 확장은 현재 미리 보기로 제공됩니다.

## <a name="prerequisites"></a>필수 구성 요소

Azure 구독이 아직 없는 경우 시작하기 전에 [Azure 체험 계정](https://azure.microsoft.com/free/)을 만듭니다.

다음과 같은 필수 조건도 필요합니다.

- [Azure Data Studio가 설치되어 있음](../download-azure-data-studio.md)
- [Azure Data Explorer 클러스터 및 데이터베이스](https://docs.microsoft.com/azure/data-explorer/create-cluster-database-portal).

## <a name="install-the-kusto-kql-extension"></a>Kusto(KQL) 확장 설치

Azure Data Studio에서 Kusto(KQL) 확장을 설치하려면 아래 단계를 수행합니다.

1. Azure Data Studio에서 확장 관리자를 엽니다. 확장 아이콘을 선택하거나 보기 메뉴에서 **확장**을 선택할 수 있습니다.

2. 검색 창에 *Kusto*를 입력합니다.

3. **Kusto(KQL)** 확장을 선택하고 세부 정보를 확인합니다.

4. **설치**를 선택합니다.

:::image type="content" source="media/kusto-extension/kusto-extension-icon.png" alt-text="Kusto 확장":::

## <a name="how-to-connect-to-an-azure-data-explorer-cluster"></a>Azure Data Explorer 클러스터에 연결하는 방법

### <a name="find-your-azure-data-explorer-cluster"></a>Azure Data Explorer 클러스터 찾기

[Azure Portal](https://ms.portal.azure.com/#home)에서 Azure Data Explorer 클러스터를 찾은 다음, 클러스터의 URI를 찾습니다.

:::image type="content" source="media/kusto-extension/kusto-extension-adx-cluster-uri.png" alt-text="URI":::

그러나 *help.kusto.windows.net* 클러스터를 사용하여 즉시 시작할 수 있습니다.

이 문서에서는 help.kusto.windows.net 클러스터의 데이터를 샘플에 사용합니다.

### <a name="connection-details"></a>연결 세부 정보

연결할 Azure Data Explorer 클러스터를 설정하려면 아래 단계를 수행합니다.

1. **연결** 창에서 **새 연결**을 선택합니다.

2. **연결 세부 정보**를 입력합니다.
    1. **연결 형식**에서 *Kusto*를 선택합니다.
    2. **클러스터**에 해당 Azure Data Explorer 클러스터를 입력합니다.

        > [!Note]
        > 클러스터 이름을 입력할 때 `https://` 접두사나 후행 `/`를 포함하지 않도록 합니다.

    3. **인증 형식**에서 기본값인 *Azure Active Directory - MFA 계정을 사용한 유니버설*을 사용합니다.
    4. **계정**에서 해당 계정 정보를 사용합니다.
    5. **데이터베이스**에서 ‘기본값’을 사용합니다.
    6. **서버 그룹**에서 ‘기본값’을 사용합니다.
        1. 이 필드를 사용하여 해당 서버를 특정 그룹으로 구성할 수 있습니다.
    7. **이름(선택 사항)** 은 비워 둡니다.
        1. 이 필드를 사용하여 서버에 별칭을 지정할 수 있습니다.

    :::image type="content" source="media/kusto-extension/kusto-extension-connection-details.png" alt-text="연결 세부 정보":::

## <a name="how-to-query-an-azure-data-explorer-database-in-azure-data-studio"></a>Azure Data Studio에서 Azure Data Explorer 데이터베이스를 쿼리하는 방법

이제 Azure Data Explorer 클러스터에 대한 연결을 설정했으므로 Kusto(KQL)를 사용하여 데이터베이스를 쿼리할 수 있습니다.

새 쿼리 탭을 만들려면 **파일 > 새 쿼리**를 선택하거나, *Ctrl+N*을 사용하거나, 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.

새 쿼리 탭이 열리면 Kusto 쿼리를 입력합니다.

다음은 KQL 쿼리의 몇 가지 샘플입니다.

```kusto
StormEvents
| limit 1000
```

```kusto
StormEvents
| where EventType == "Waterspout"
```

KQL 쿼리를 작성하는 방법에 대한 자세한 내용은 [Azure Data Explorer에 대한 쿼리 작성](https://docs.microsoft.com/azure/data-explorer/write-queries#overview-of-the-query-language)을 참조하세요.

## <a name="view-extension-settings"></a>확장 설정 보기

Kusto 확장 설정을 변경하려면 아래 단계를 수행합니다.

1. Azure Data Studio에서 확장 관리자를 엽니다. 확장 아이콘을 선택하거나 보기 메뉴에서 **확장**을 선택할 수 있습니다.

2. **Kusto(KQL)** 확장을 찾습니다.

3. **관리** 아이콘을 선택합니다.

4. **확장 설정** 아이콘을 선택합니다.

확장 설정은 다음과 같이 표시됩니다.

:::image type="content" source="media/kusto-extension/kusto-extension-settings.png" alt-text="Kusto(KQL) 확장 설정":::

## <a name="sanddance-visualization"></a>SandDance 시각화

Azure Data Studio의 KQL(Kusto) 확장을 사용하는 [SandDance 확장](https://docs.microsoft.com/sql/azure-data-studio/sanddance-extension)은 다양한 대화형 시각화를 결합합니다. KQL 쿼리 결과 집합에서 **시각화 도우미** 단추를 선택하여 [SandDance](https://sanddance.js.org/)를 시작합니다.

:::image type="content" source="media/kusto-extension/kusto-extension-sanddance-demo.gif" alt-text="SandDance 시각화":::

## <a name="limitations-and-considerations"></a>제한 사항 및 고려 사항

- Kusto 쿼리를 실행하기 전에 Azure Data Explorer 클러스터에 대한 데이터베이스를 선택해야 합니다.
- Azure Data Explorer 클러스터를 너무 오랫동안 유휴 상태로 두면 연결이 끊어질 수 있습니다.
    - 해결 방법: 클러스터에서 연결을 끊고 다시 연결합니다.

## <a name="next-steps"></a>다음 단계

- [Kusto Notebook 만들기 및 실행](../notebooks/notebooks-kusto-kernel.md)
- [Azure Data Studio의 Kqlmagic Notebook](../notebooks-kqlmagic.md)
- [SQL 대 Kusto 참고 자료](https://docs.microsoft.com/azure/data-explorer/kusto/query/sqlcheatsheet)
- [Azure 데이터 탐색기란?](https://docs.microsoft.com/azure/data-explorer/data-explorer-overview)
- [SandDance 시각화 사용](https://sanddance.js.org/)
