---
title: SQL 설명서 버전 관리 시스템| Microsoft Docs
ms.date: 10/15/2019
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: conceptual
ms.reviewer: ''
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||>=sql-server-linux-2017||=sql-server-previousversions||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f175e9639b07c945b92b6fd715fa8b34ebea60c3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73049913"
---
# <a name="versioning-system-for-sql-documentation"></a>SQL 설명서용 버전 관리 시스템

[!INCLUDE[includes_appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

이 문서에서는 SQL 설명서의 _버전 관리 시스템_에 대해 설명합니다. 버전 관리 시스템은 제품 및 해당 버전을 인식합니다. 이 시스템에서는 원하는 제품 및 버전을 선택할 수 있습니다. 그러면 해당 설명서가 표시됩니다.

## <a name="applies-to-products"></a>적용 대상 제품

대부분의 SQL Server 아티클에는 제목 아래에 **적용 대상**이 표시됩니다. 같은 줄에서 아티클과 제품의 관련성을 나타내는 편리한 SQL _제품_ 목록이 표시됩니다. 예를 들어, 제품 SQL Server는 해당 아티클과 관련된 것으로 표시될 수 있지만, Azure SQL Database는 관련이 없는 것으로 표시될 수 있습니다.

**적용 대상** 줄에는 제품의 _버전_에 대한 정보가 없습니다. 버전 관리 시스템 구성의 **적용 대상** 줄과 제품 측면 간이 맞지 않는 경우를 방지하기 위해 노력하고 있습니다.

## <a name="history-of-separate-file-sets"></a>별도의 파일 세트 기록

SQL Server 2014 및 이전 버전의 경우 각 버전에는 설명서 파일의 고유한 전체 복사본이 있습니다. 예를 들어, SQL Server 2014용 설명서는 SQL Server 2012 설명서의 복사본으로 시작됩니다. 그러면 제품 개발 주기 동안 2014 사본이 편집됩니다.

이러한 이전 접근 방식을 사용하면 2014 설명서에서 결함이 발견될 경우 해당 결함이 2012 및 2008에도 나타날 수 있게 됩니다. 이로 인해 결함 수정 및 일반적인 유지 관리가 어려워집니다.

## <a name="multiple-versions-in-the-same-files"></a>동일한 파일의 여러 버전

이러한 이유로 SQL Server 2016용 설명서 파일은 2017, 2019에도 해당되며 \<vNext\>에도 해당될 수 있습니다. 이제 SQL Server 설명서 파일에 _버전 관리 모니커_를 할당하게 되므로 이러한 통합이 좀 더 실질적으로 이루어질 수 있습니다. 버전 관리 모니커가 지정된 각 설명서 파일에 대해 의미가 있는 모든 세분성 수준에서 할당되거나 명시적으로 포함됩니다.

## <a name="versioning-control-in-the-ui"></a>UI의 버전 제어

:::no-loc text="Docs"::: 웹 사이트를 사용하여 SQL 설명서 아티클을 볼 때 현재 선택한 버전 관리 모니커는 TOC(목차) 위에 표시됩니다. 컨트롤은 드롭다운 목록입니다.

![media_versioning-control-10-sql-server-2017.png](media/versioning-control-10-sql-server-2017.png)

다른 버전의 SQL Server에 대한 설명서를 보려는 경우 현재 버전 모니커의 끝에 있는 확장 화살표를 클릭합니다. 그런 다음, 원하는 제품 및 버전 조합을 클릭하여 선택합니다. 다른 버전을 클릭하면 표시된 설명서가 갑자기 변경되어 새로 선택한 버전의 차이점을 표시합니다. 변경 내용이 있을 수도 있고 없을 수도 있으며, 두 경우 모두 일반적입니다.

![media_versioning-control-20-expanded.png](media/versioning-control-20-expanded.png)

### <a name="https-parameter-no-loc-textview"></a>HTTPS 매개 변수 :::no-loc text="view=":::

웹 주소가 `https://docs.microsoft.com/sql/`로 시작하는 각 아티클의 주소에는 `?view=`라는 매개 변수가 추가되어 있습니다. 이 매개 변수 값은 버전 관리 모니커 코드입니다.

`https` 주소의 모니커 _코드_는 버전 관리 컨트롤에 표시되는 모니커 _name_과 항상 일치합니다.

## <a name="products-not-editions"></a>제품, 에디션 아님

### <a name="editions"></a>에디션

1990년대부터 2000년대에 접어들면서 Microsoft SQL Server는 1개의 제품만 있었습니다. 각 SQL Server 버전에는 SQL Server 2008 _Developer_ 및 _Enterprise_ 버전과 같은 다양한 _버전_이 있었습니다. 에디션은 약간 다른 기능 세트를 제공하지만 코어 제품은 동일했습니다. 새 SQL Server 릴리스에는 여전히 다양한 에디션이 있을 수 있습니다.

### <a name="products"></a>Products

최근 들어 클라우드 컴퓨팅 및 Microsoft Azure의 사용이 증가하면서 Microsoft는 Azure SQL Database 제품을 출시했습니다. 기존 SQL Server 온-프레미스 제품과 Azure SQL Database 제품은 많은 코드를 공유하지만, 이러한 제품은 실제로 두 가지 별도 제품입니다.

SQL의 경우 에디션 간에는 버전 관리 모니커가 다르지 않지만 제품 간에는 다릅니다.

#### <a name="azure-cloud-sql-products"></a>Azure 클라우드 SQL 제품

전체 웹 주소가 `https://docs.microsoft.com/sql/`로 시작되는 문서의 경우 거의 모든 항목이 SQL Server라는 하나 이상의 제품 버전에 적용됩니다. 이러한 아티클의 많은 하위 세트는 Azure 클라우드에서 호스트되는 SQL 서비스 제품 중 하나 이상에도 적용됩니다. 이러한 SQL 클라우드 제품 중 하나가 Azure SQL Database입니다.

기본적으로 Azure SQL Database 제품에는 버전이 하나만 있습니다. Azure SQL Database에만 적용되고 SQL Server에는 적용되지 않는 거의 모든 아티클은 웹 주소가 `https://docs.microsoft.com/azure/sql-database/`로 시작됩니다.

## <a name="scenarios-of-version-filtering"></a>버전 필터링 시나리오

버전 관리 시스템은 현재 활성 모니커에 적용되지 않는 모든 설명서 콘텐츠를 필터링하여 작동합니다. 다른 버전 관리 모니커를 선택할 때마다 숨겨진 콘텐츠 세트가 변경됩니다. 필터링은 다음 수준에서 콘텐츠를 숨깁니다.

- 아티클 내의 섹션 또는 문장
- TOC(목차)에서 아티클에 대한 항목

다음은 다른 모니커를 선택할 때의 결과를 설명하는 시나리오입니다.

### <a name="scenario-1-within-the-current-article"></a>시나리오 1: 현재 문서 내

다음 시나리오는 현재 아티클 내의 섹션에 중점을 둡니다.

1. 현재 버전 관리 모니커는 **SQL Server 2017**입니다.
2. SQL Server 버전 2017에 처음 추가된 기능을 설명하는 섹션을 읽고 있습니다.
3. 모니커를 **SQL Server 2016**으로 변경합니다.
4. 읽던 섹션이 없어진 것을 알 수 있습니다.
5. 모니커를 다시 변경합니다. 이번에는 **SQL Server 2019**로 변경합니다.
6. 읽고 있던 2017 섹션이 다시 표시됩니다.

위의 시나리오에서 새 2017 기능은 다음 모니커 코드를 포함하는 _모니커 범위_로 표시될 수 있습니다.

- `>=sql-server-2017`

모니커 **SQL Server 2019**를 선택하면 버전 관리 시스템에서 2019를 2017보다 크거나 같다고 인식하고 해당 섹션을 표시합니다.

### <a name="scenario-2-click-a-link-to-a-hidden-article"></a>시나리오 2: 숨겨진 아티클에 대한 링크 클릭

다음의 일반적이지 않은 시나리오는 TOC(목차)에서 현재 숨겨진 아티클에 대한 링크를 클릭하면 어떻게 되는지 설명합니다. 간단히 말해서 링크는 다음과 같이 작동합니다.

1. 현재 버전 관리 모니커는 **SQL Server 2017**입니다.
2. 현재 아티클 :::no-loc text="A":::에서 SQL Server 2016에만 적용되는 아티클 :::no-loc text="B":::에 대한 링크를 클릭합니다.
    - 클릭하기 전에 목차에는 숨겨진 :::no-loc text="B"::: 아티클에 대한 항목이 있습니다.
3. 클릭하면 아티클 :::no-loc text="B":::가 표시됩니다.
    - 아티클 :::no-loc text="B":::가 표시되면 버전 관리 컨트롤이 **SQL Server 2016** 모니커로 전환됩니다.
    - 원본 모니커 **SQL Server 2017**은 중단되어야 하기 때문입니다. 이러한 중단으로 인해 웹 페이지의 위쪽에 정보 메시지가 표시됩니다. [메시지](#anchor-message-unavailable-for-moniker)는 새 아티클 :::no-loc text="B":::를 수용하도록 현재 모니커를 전환해야 함을 설명합니다.

### <a name="scenario-3-navigate-to-an-https-address"></a>시나리오 3: https 주소 이동

다음 아티클은 SQL Server 2017용으로 새로 추가되었습니다. 이 아티클은 버전 2017의 SQL Server에 추가된 기능을 설명합니다. 이러한 새 기능의 대부분이 버전 2019에도 포함되어 있습니다. 아티클의 특성은 다음과 같습니다.

| attribute | 값 |
| :-------- | :---- |
| 제목 | SQL Server 2017의 새로운 기능 |
| 모니커 범위 | `>= sql-server-2017 || = sqlallproducts-allversions` |
| `https` 주소 | `https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017` |
| &nbsp; | &nbsp; |

기본 `https` 주소가 지정된 경우 다음 표에서는 사용자가 `?view=` 매개 변수에 다양한 값을 추가할 때 발생하는 결과를 설명합니다.

| `?view=`의 값 | `https` 주소 탐색 동작 |
| :---------------- | :------------------------------ |
| _(매개 변수 없음)_ | 버전 관리 시스템에서 기본 모니커 값을 시도합니다. 일반적으로 이 값을 SQL Server의 미리 보기가 아닌 최신 버전으로 설정합니다.<br/><br/>SQL Server 2017 또는 2019의 기본값은 특성 `>= sql-server-2017`을 충족합니다.<br/><br/>시스템은 `?view=sql-server-2017`과 같이 `https` 주소에 매개 변수를 추가합니다.<br/>그러면 버전 관리 드롭다운 목록 컨트롤이 일치하는 모니커 이름으로 설정됩니다. |
| `sql-server-2016` | 버전 관리 시스템은 아티클의 모니커 범위에 버전 2016이 포함되지 않는다는 것을 인식합니다.<br/><br/>따라서 시스템은 해당 범위를 만족하는 모니커 중 하나를 선택합니다.<br/><br/>버전 2016의 경우와 마찬가지로 매개 변수 `?view=`가 추가되고 컨트롤 이름이 매개 변수 값과 일치합니다. |
| `sql-server-2017` | 버전 관리 시스템은 매개 변수 값이 아티클의 모니커 범위에 포함되어 있음을 이해합니다.<br/><br/>버전 관리 컨트롤은 매개 변수 값과 일치하도록 설정됩니다. |
| `sql-server-2019` | 매개 변수와 컨트롤이 2019로 설정된 경우를 제외하고 `sql-server-2017` 값의 경우도 동일합니다. |
| &nbsp; | &nbsp; |

### <a name="all-sql---hide-nothing-special-moniker"></a><a name="anchor-allsql-hidenothing"></a> 모든 SQL - 모두 표시, 특수 모니커

**모든 SQL**의 특별한 모니커 제품 이름은 하나이며 유일한 버전은 **모두 표시**입니다. 이 모니커는 특정 변경 내용을 내부적으로 테스트하기 위한 것입니다. 고객이 이 모니커를 사용할 경우 유익하기보다 오해를 일으킬 가능성이 높습니다.

일부 아티클에는 여러 버전의 SQL Server 관련 정보가 포함되어 있습니다. 모든 일반 모니커는 모니커 버전에 대해 부정확하거나, 혼동을 일으키거나, 모순되는 정보를 표시할 수 있는 버전 관련 섹션을 숨깁니다. 특별한 **모든 SQL** 모니커는 모든 버전 섹션을 표시하며, 부정확한 정보가 표시되고 있음을 명확하게 나타내지 않을 수 있습니다.

## <a name="message-the-requested-page-is-not-available-for-moniker"></a><a name="anchor-message-unavailable-for-moniker"></a> 메시지: 요청된 페이지를 \<모니커\>에 사용할 수 없습니다.

다음 시나리오에서는 :::no-loc text="Docs"::: 웹 페이지 맨 위에 있는 정보 메시지를 표시합니다.

1. 현재 버전 관리 모니커는 **SQL Server 2017**입니다.
2. SQL Server 2017과 관련된 아티클을 읽고 있습니다.
    - 이 아티클은 제품 Azure SQL Database와 관련이 _없습니다_.
3. 모니커를 **Azure SQL Database - 최신**으로 변경하려고 합니다.
4. 그러면 해당 시도가 거부되고 메시지가 표시됩니다.

이 시나리오의 끝부분에서는 Docs 웹 페이지의 위쪽에 다음과 같은 정보 메시지가 표시됩니다.

> 요청한 페이지를 현재 Azure SQL Database - 최신에서 사용할 수 없습니다. 이 페이지를 사용할 수 있는 최신 제품 버전으로 리디렉션되었습니다.

_최신_ 버전은 아직 완전히 릴리스되지 않았으며 _미리 보기_ 상태에 있는 버전을 제외할 수 있습니다.

![media_versioning-control-30-viewfallbackfrom.png](media/versioning-control-30-viewfallbackfrom.png)

## <a name="previous-versions-of-sql-server"></a>SQL Server 이전 버전

버전 관리 시스템은 SQL Server 버전 2016부터 완전히 구현됩니다.

- _2012 및 이전 버전:_ &nbsp; 버전 관리 시스템은 SQL Server 2012 이전 버전에는 사용되지 않습니다.
    - **SQL Server - 이전**의 특별한 모니커는 거의 모든 문서를 숨기기 위한 것입니다. 드물지만 예외적으로 이전 버전의 고객에게 한 번만 필요할 수 있는 아티클도 일부 있습니다.
    - [SQL Server 이전 버전, 2012-2005](../toc/previous-versions-sql-server.md)

- _2014:_ &nbsp; 버전 관리 시스템은 SQL Server 2014에서는 절반 정도 구현됩니다. 버전 관리 컨트롤에서 SQL Server 2014를 선택할 수 있으며 문제없이 작동합니다. 그러나 기본적으로 2014용 파일은 2014 전용이고, 마찬가지로 2008용 파일도 2008 전용입니다.
    - [SQL Server 2014 설명서](/sql/2014-toc/books-online-for-sql-server-2014?view=sql-server-2014)

- _2016 이상:_ &nbsp; 버전 관리 시스템은 SQL Server 2016 이상 버전에 대해 완전히 구현됩니다.
    - [SQL Server 설명서 2016 이상 시작](/sql/sql-server/?view=sql-server-2016)

## <a name="see-also"></a>참고 항목

[SQL Server 이전 버전, 2014-2005](../toc/previous-versions-sql-server.md)  
[SQL Server 설명서 탐색 가이드](sql-docs-navigation-guide.md)  
[SQL Server 설명서에 기여하는 방법](sql-server-docs-contribute.md)  
