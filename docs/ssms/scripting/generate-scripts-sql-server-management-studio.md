---
title: 스크립트 생성
description: 스크립트 생성 및 게시 마법사를 사용하여 여러 개체에 대한 Transact-SQL 스크립트를 만드는 방법과 개체 탐색기 메뉴를 사용하여 개별 개체 또는 여러 개체에 대한 스크립트를 생성하는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: markingmyname
ms.author: maghan
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.date: 04/07/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 76d942c643b510f956f5199920c228e4071795e8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480654"
---
# <a name="generate-scripts-sql-server-management-studio"></a>스크립트 생성(SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 생성하는 두 가지 메커니즘을 제공합니다. **스크립트 생성 및 게시 마법사** 를 사용하여 여러 개체에 대한 스크립트를 만들 수 있습니다. 또한 **개체 탐색기** 에서 **스크립팅** 메뉴를 사용하여 개별 개체 또는 여러 개체에 대한 스크립트를 생성할 수도 있습니다.

SSMS(SQL Server Management Studio)를 사용하여 다양한 개체를 스크립팅하는 방법에 대한 자세한 자습서는 [자습서: SSMS에서 스크립팅](../tutorials/scripting-ssms.md)을 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에

요구 사항에 가장 적합한 메커니즘을 선택합니다. 

###  <a name="generate-and-publish-scripts-wizard"></a><a name="GenPubScriptWiz"></a> 스크립트 생성 및 게시 마법사

**스크립트 생성 및 게시 마법사** 를 사용하여 다양한 개체에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 만들 수 있습니다. 이 마법사는 데이터베이스의 모든 개체 또는 사용자가 선택한 개체의 하위 집합에 대한 스크립트를 생성합니다. 이 마법사에는 사용 권한, 데이터 정렬, 제약 조건 등을 포함할지 여부와 같은 여러 스크립트 옵션이 있습니다. 마법사를 사용하는 방법은 [Generate and Publish Scripts Wizard](./generate-and-publish-scripts-wizard.md)를 참조하십시오.
  
### <a name="object-explorer-script-as-menu"></a><a name="OEScriptAsMenu"></a> 개체 탐색기 스크립팅 메뉴

**개체 탐색기 스크립팅** 메뉴를 사용하여 단일 개체, 여러 개체 또는 단일 개체에 대한 여러 명령문을 스크립팅할 수 있습니다. 여러 스크립트 유형 중 하나를 선택할 수 있습니다. 예를 들어 개체를 만들거나 변경하거나 삭제할 수 있습니다. 쿼리 편집기 창의 스크립트를 파일이나 클립보드에 저장할 수 있습니다. 스크립트는 유니코드 형식으로 만들어집니다.

## <a name="to-generate-a-script-of-a-single-object"></a><a name="ScriptSingleObject"></a> 단일 개체의 스크립트를 생성하려면

**단일 개체를 스크립팅하려면**

1. 개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2. **데이터베이스** 를 확장한 다음 스크립팅할 개체가 포함된 데이터베이스를 확장합니다.

3. 개체의 범주를 확장합니다. 예를 들어 **테이블** 또는 **뷰** 노드를 확장합니다.

4. 개체를 마우스 오른쪽으로 클릭하여 **\<object type> 스크립팅** 을 가리킵니다. 예를 들어 **테이블 스크립팅** 을 가리킵니다.

5. 스크립트 유형을 가리킵니다(예: **CREATE** 또는 **ALTER**).

6. 스크립트를 저장할 위치를 선택합니다(예: **새 쿼리 편집기 창** 또는 **클립보드**).

    ![테이블 스크립팅](media/generate-scripts-sql-server-management-studio/script-table.png)

**개체 탐색기 정보** 창을 사용하여 동일한 범주의 여러 개체에 대한 스크립트를 생성할 수 있습니다.

1. 개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2. **데이터베이스** 를 확장한 다음 스크립팅할 개체가 포함된 데이터베이스를 확장합니다.

3. 스크립팅할 개체 유형의 범주 노드(예: **테이블** 노드)로 이동합니다.

4. **F7** 을 선택하거나 **보기** 메뉴를 열고 **개체 탐색기 정보** 를 선택하여 **개체 탐색기 정보** 창을 엽니다.

    ![보기 메뉴](media/generate-scripts-sql-server-management-studio/object-explorer-details-view-menu.png)

5. 스크립팅할 개체 중 하나를 마우스 왼쪽 단추로 클릭합니다.

6. Ctrl 키를 누른 채로 스크립팅할 두 번째 개체를 클릭합니다.

7. 선택한 개체 중 하나를 마우스 오른쪽 단추로 클릭하고 **\<object type> 스크립팅** 을 선택합니다.

    ![세부 정보](media/generate-scripts-sql-server-management-studio/object-explorer-details.png)