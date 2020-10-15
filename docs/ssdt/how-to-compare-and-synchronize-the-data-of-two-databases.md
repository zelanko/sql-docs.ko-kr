---
title: 두 데이터베이스의 데이터 비교 및 동기화
description: 두 데이터베이스의 데이터를 비교하고 동기화하는 방법을 알아봅니다. 비교를 설정하고, 차이점을 확인하고, 대상을 업데이트하는 방법을 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.connection.datasources.f1
- sql.data.tools.datacompare.watermark.f1
- sql.data.tools.datacompare.connection.objectselection.f1
ms.assetid: 2148e517-ed42-41c6-b753-1ac625f594c8
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: e246374476c3dff300aaf6c53ee3c6e8a1896db5
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987979"
---
# <a name="how-to-compare-and-synchronize-the-data-of-two-databases"></a>방법: 두 데이터베이스의 데이터 비교 및 동기화

두 데이터베이스에 포함된 데이터를 비교할 수 있습니다. 비교하는 데이터베이스는 각각 ‘원본’ 및 ‘대상’이라고 합니다.   
  
> [!NOTE]  
> ‘데이터베이스 프로젝트’ 및 .dacpac 또는 .bacpac 패키지는 데이터 비교 시 원본 또는 대상이 될 수 없습니다.  
  
데이터를 비교할 때는 대상 데이터베이스의 데이터 일부 또는 모두를 업데이트하여 차이가 있는 데이터베이스를 동기화하는 데 사용할 수 있는 ‘DML(데이터 조작 언어)’ 스크립트가 생성됩니다.** 데이터 비교가 완료되면 결과가 Visual Studio의 [데이터 비교] 창에 표시됩니다.  
  
비교가 완료된 후에는 다른 단계를 수행할 수 있습니다.  
  
-   두 데이터베이스 간의 차이를 볼 수 있습니다. 자세한 내용은 [데이터 차이 보기](#ViewDifferences)를 참조하세요.  
  
-   원본과 일치하도록 대상의 모두 또는 일부를 업데이트할 수 있습니다. 자세한 내용은 [데이터베이스 데이터 동기화](#Synchronize)를 참조하세요.  
  
자세한 내용은 [하나 이상의 테이블에 있는 데이터를 참조 데이터베이스에 있는 데이터와 비교하고 동기화](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)를 참조하세요.  
  
> [!NOTE]  
> 또한 두 데이터베이스 또는 동일 데이터베이스의 두 버전의 ‘스키마’를 비교할 수 있습니다. 자세한 내용은 [방법: 스키마 비교를 사용하여 서로 다른 데이터베이스 정의 비교](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)를 참조하세요.  
  
## <a name="comparing-database-data"></a><a name="CompareDatabaseData"></a>데이터베이스 데이터 비교  
  
#### <a name="to-compare-data-by-using-the-new-data-comparison-wizard"></a>새 데이터 비교 마법사를 사용해서 데이터를 비교하려면  
  
1.  **SQL** 메뉴에서 **데이터 비교**를 가리킨 후 **새 데이터 비교**를 클릭합니다.  
  
    새 데이터 비교 마법사가 나타납니다. 또한 [데이터 비교] 창이 열리고 Visual Studio가 DataCompare1과 같은 이름을 자동으로 할당합니다.  
  
2.  원본 및 대상 데이터베이스를 식별합니다.  
  
    **원본 데이터베이스** 목록 또는 **대상 데이터베이스** 목록이 비어 있으면 **새 연결**을 클릭합니다. **연결 속성** 대화 상자에서 데이터베이스가 있는 서버 및 데이터베이스에 연결할 때 사용할 인증 유형을 식별합니다. 그런 후 **확인**을 클릭하여 **연결 속성** 대화 상자를 닫고 데이터 비교 마법사로 돌아갑니다.  
  
    데이터 비교 마법사의 첫 번째 페이지에서 각 데이터베이스의 정보가 올바른지 확인하고, 결과에 포함하려는 레코드를 지정한 후 **다음**을 클릭합니다. 데이터 비교 마법사의 두 번째 페이지가 나타나고 데이터베이스에 있는 테이블 및 뷰가 계층적 목록으로 표시됩니다.  
  
3.  비교하려는 테이블 및 뷰에 대해 확인란을 선택합니다. 필요에 따라 데이터베이스 개체 노드를 확장한 후 비교하려는 개체 내의 열에 대한 확인란을 선택합니다.  
  
    > [!NOTE]  
    > 테이블 및 뷰가 목록에 표시되기 위해서는 두 가지 조건을 충족해야 합니다. 첫째, 개체의 스키마가 원본 및 대상 데이터베이스 간에 일치해야 합니다. 둘째, 기본 키, 고유 키, 고유 인덱스 또는 고유 제약 조건을 포함하는 테이블 및 뷰만 목록에 표시됩니다. 두 조건을 충족하는 테이블 또는 뷰가 없으면 목록이 비어 있습니다.  
  
4.  두 개 이상의 키가 있으면, **비교 키** 열을 사용해서 데이터 비교 기준으로 사용할 키를 지정할 수 있습니다. 예를 들어 기본 키 열 또는 다른(고유하게 식별 가능한) 키 열을 기준으로 비교를 수행할지를 지정할 수 있습니다.  
  
5.  **Finish**를 클릭합니다.  
  
    비교가 시작됩니다.  
  
    > [!NOTE]  
    > 진행 중인 데이터 비교 작업을 중지하려면 **SQL** 메뉴를 열고 **데이터 비교**를 클릭한 후 **데이터 비교 중지**를 클릭하면 됩니다.  
  
    비교가 완료되면 두 데이터베이스 간의 데이터 차이를 볼 수 있습니다. 또한 원본 데이터베이스의 데이터와 일치하도록 대상 데이터베이스의 일부 또는 모든 데이터를 업데이트할 수도 있습니다.  
  
#### <a name="to-compare-data-by-using-the-visual-studio-automation-model"></a>Visual Studio 자동화 모델을 사용해서 데이터를 비교하려면  
  
1.  **보기** 메뉴를 열고 **다른 창**을 가리킨 후 **명령 창**을 클릭합니다.  
  
2.  명령 창에서 다음 명령을 입력합니다.  
  
    ```  
    Sql.NewDataComparison /SrcServerName sServerName /SrcDatabaseName sDatabaseName /SrcUserName sUserName /SrcPassword sPassword /SrcDisplayName sDisplayName /TargetServerName tServerName /TargetDatabaseName tDatabaseName /TargeUserName tUserName /TargetPassword tPassword /TargetDisplayName tDisplayName  
    ```  
  
    자리 표시자(*sServerName*, *sDatabaseName*, *sUserName*, *sPassword*, *sDisplayName*, *tServerName*, *tDatabaseName*, *tUserName*, *tPassword* 및 *tDisplayName*)를 원본 및 대상 데이터베이스에 대한 값으로 바꿉니다.  
  
    원본 및 대상을 지정하지 않으면 **새 데이터 비교** 대화 상자가 나타납니다. Sql.NewDataComparison 명령의 매개 변수에 대한 자세한 내용은 [Visual Studio Team System의 데이터베이스 기능에 대한 Automation 명령 참조](/previous-versions/visualstudio/visual-studio-2010/dd470565(v=vs.100))를 참조하세요.  
  
    지정된 원본 및 대상 데이터베이스의 데이터가 비교됩니다. 결과는 데이터 비교 세션에 표시됩니다. 결과를 보거나 데이터를 동기화하는 방법에 대한 자세한 내용은 [데이터 차이 보기](#ViewDifferences) 및 [데이터베이스 데이터 동기화](#Synchronize)를 참조하세요.  
  
## <a name="viewing-data-differences"></a><a name="ViewDifferences"></a>데이터 차이 보기  
두 데이터베이스의 데이터를 비교한 후에는 데이터 비교에 사용자가 비교한 각 ‘데이터베이스 개체’ 및 해당 상태가 나열됩니다. 또한 상태별로 그룹화된 각 개체 내에서 레코드에 대한 결과를 볼 수도 있습니다. 상태 지정에 대한 자세한 내용은 [하나 이상의 테이블에 있는 데이터를 참조 데이터베이스에 있는 데이터와 비교 및 동기화](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)를 참조하세요.  
  
차이를 확인한 후에는 서로 다르거나, 누락되었거나, 새로 추가된 개체 또는 레코드의 일부 또는 전체가 원본과 일치하도록 대상을 업데이트할 수 있습니다. 자세한 내용은 [데이터베이스 데이터 동기화](#Synchronize)를 참조하세요.  
  
#### <a name="to-view-data-differences"></a>데이터 차이를 보려면  
  
1.  원본 및 대상 데이터베이스의 데이터를 비교합니다. 자세한 내용은 [데이터베이스 데이터 비교](#CompareDatabaseData)를 참조하세요.  
  
2.  (선택 사항) 다음 중 하나 또는 모두를 수행합니다.  
  
    -   기본적으로 상태에 관계없이 모든 개체에 대한 결과가 표시됩니다. 특정 상태의 개체만 표시하려면 **필터** 목록에서 옵션을 클릭합니다.  
  
    -   특정 개체 내의 레코드에 대한 결과를 보려면 기본 결과 창에서 개체를 클릭한 후 레코드 보기 창에서 탭을 클릭합니다. 각 탭에는 특정 상태(서로 다름, 원본에만 있음, 대상에만 있음 및 동일함)의 개체 내에 있는 모든 레코드가 표시됩니다. 데이터는 레코드 및 열을 기준으로 표시됩니다.  
  
## <a name="synchronizing-database-data"></a><a name="Synchronize"></a>데이터베이스 데이터 동기화  
두 데이터베이스의 데이터를 비교한 후에는 원본과 일치하도록 대상의 전체 또는 일부를 업데이트하여 서로 동기화할 수 있습니다. 두 가지 유형의 데이터베이스 개체(테이블 및 뷰)의 데이터를 비교할 수 있습니다.  
  
#### <a name="to-update-target-data-by-using-the-write-updates-command"></a>업데이트 쓰기 명령을 사용해서 대상 데이터를 업데이트하려면  
  
1.  원본 및 대상 데이터베이스의 데이터를 비교합니다. 자세한 내용은 [데이터베이스 데이터 비교](#CompareDatabaseData)를 참조하세요.  
  
    비교가 완료되면 데이터 비교 창에 비교된 개체의 결과가 나열됩니다. 4개 열(다른 레코드, 원본에만 있음, 대상에만 있음 및 동일한 레코드)에 동일하지 않은 개체에 대한 정보가 표시됩니다. 각 개체에 대해 발견된 다른 레코드 수, 업데이트 작업으로 변경될 수 있는 레코드 수가 해당 열에 표시됩니다. 이러한 두 값은 처음에 일치하지만 4단계에서 사용자가 업데이트할 개체를 변경할 수 있습니다.  
  
    자세한 내용은 [하나 이상의 테이블에 있는 데이터를 참조 데이터베이스에 있는 데이터와 비교하고 동기화](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)를 참조하세요.  
  
2.  데이터 비교 창의 테이블에서 행을 클릭합니다.  
  
    세부 정보 창에는 사용자가 클릭한 데이터베이스 개체의 레코드에 대한 결과가 표시됩니다. 레코드는 상태별로 탭에 그룹화되며, 이를 사용해서 원본에서 대상으로 전파할 데이터를 지정할 수 있습니다.  
  
3.  세부 정보 창에서 이름에 0이 아닌 다른 숫자가 포함된 탭을 클릭합니다.  
  
    **대상에만 있음** 테이블의 **업데이트** 열에는 업데이트할 행을 선택할 수 있는 확인란이 있습니다. 기본적으로 각 확인란이 선택되어 있습니다.  
  
4.  원본의 데이터로 대상의 레코드를 업데이트하지 않으려면 해당 확인란을 지웁니다.  
  
    확인란을 지우면 업데이트할 레코드 수가 줄어들고 해당 작업에 맞게 표시가 변경됩니다. 이 숫자는 1단계의 설명에 따라 세부 정보 창의 상태 표시줄 및 기본 결과 창의 해당 열에 표시됩니다.  
  
5.  (선택 사항) **스크립트 생성**을 클릭합니다.  
  
    Transact\-SQL 편집기 창이 열리고 대상을 업데이트하는 데 사용되는 ‘DML(데이터 조작 언어)’ 스크립트가 표시됩니다.  
  
6.  서로 다르거나, 누락되었거나, 새로 추가된 레코드를 동기화하려면 **대상 업데이트**를 클릭합니다.  
  
    > [!NOTE]  
    > 대상 데이터베이스를 업데이트하는 동안에는 **대상에 쓰기 중지**를 클릭하여 작업을 취소할 수 있습니다.  
  
    대상에서 선택한 레코드의 데이터가 원본의 해당 레코드의 데이터로 업데이트됩니다.  
  
    > [!NOTE]  
    > 인덱싱된 뷰를 업데이트하도록 선택하면 이 작업으로 인해 동일한 테이블에 중복 키가 삽입될 경우 **대상 업데이트** 작업이 실패할 수 있습니다.  
  
#### <a name="to-update-target-data-by-using-a-transact-sql-script"></a>Transact\-SQL 스크립트를 사용해서 대상 데이터를 업데이트하려면  
  
1.  원본 및 대상 데이터베이스의 데이터를 비교합니다. 자세한 내용은 [데이터베이스 데이터 비교](#CompareDatabaseData)를 참조하세요.  
  
    비교가 완료되면 데이터 비교 창에 비교된 개체가 나열됩니다. 자세한 내용은 [하나 이상의 테이블에 있는 데이터를 참조 데이터베이스에 있는 데이터와 비교하고 동기화](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)를 참조하세요.  
  
2.  (선택 사항) 이전 절차의 설명에 따라 세부 정보 창에서 업데이트하지 않으려는 대상의 레코드에 대한 확인란을 지웁니다.  
  
3.  **스크립트 생성**을 클릭합니다.  
  
    대상의 데이터가 원본의 데이터와 일치하도록 만드는 데 필요한 변경 내용을 전파하는 Transact\-SQL 스크립트가 새 창에 표시됩니다. 새 창 이름은 **DataUpdate_Database_1.sql**과 같이 지정됩니다.  
  
    이 스크립트에는 세부 정보 창에서 수행한 변경 내용이 반영됩니다. 예를 들어 [dbo].[Shippers] 테이블의 대상에만 있음 페이지에서 특정 행에 대한 확인란을 지웠을 수 있습니다. 그러면 스크립트에서 해당 행이 업데이트되지 않습니다.  
  
4.  (선택 사항) **DataUpdate_Database_1.sql** 창에서 이 스크립트를 편집합니다.  
  
5.  (선택 사항이지만 권장됨) 대상 데이터베이스를 백업합니다.  
  
6.  **실행**을 클릭하여 대상 데이터베이스를 업데이트합니다.  
  
    업데이트하려는 대상 데이터베이스에 대한 연결을 지정합니다.  
  
    > [!IMPORTANT]  
    > 기본적으로 업데이트는 트랜잭션 범위 내에서 수행됩니다. 오류가 발생하면 전체 업데이트를 롤백할 수 있습니다. 이 동작은 변경할 수 있습니다.  
  
    대상에서 선택한 레코드의 데이터가 원본의 해당 레코드의 데이터로 업데이트됩니다.  
  
## <a name="see-also"></a>참고 항목  
[하나 이상의 테이블에 있는 데이터를 참조 데이터베이스에 있는 데이터와 비교 및 동기화](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)  
