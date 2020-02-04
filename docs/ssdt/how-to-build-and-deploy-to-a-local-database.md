---
title: 로컬 데이터베이스 빌드 및 배포
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: ebca8ff8-9a09-4207-8979-9d577af7c1d5
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c3c079ddc375c1fa252975c419aff587d324dd1b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241612"
---
# <a name="how-to-build-and-deploy-to-a-local-database"></a>방법: 로컬 데이터베이스 빌드 및 배포

Microsoft SQL Server 2012에서는 SQL Server 데이터베이스 프로젝트를 디버그할 때 활성화되는 SQL Server Express 로컬 데이터베이스 런타임이라는 로컬 주문형 서버 인스턴스를 제공합니다. 이 로컬 서버 인스턴스를 프로젝트를 빌드, 테스트 및 디버깅하기 위한 샌드박스로 사용할 수 있습니다. 로컬 서버 인스턴스는 설치된 SQL Server 인스턴스로부터 독립적이며, SSDT(SQL Server Data Tools) 외부에서는 액세스할 수 없습니다. 이러한 방식은 프로덕션 데이터베이스에 액세스할 수 없거나 액세스가 제한되었지만 권한이 있는 사용자가 프로젝트를 프로덕션에 배포하기 전에 로컬로 프로젝트를 테스트하려는 개발자에게 유용합니다. 또한 SQL Azure용 데이터베이스 솔루션을 개발할 때 이 로컬 서버에서 제공하는 편리한 기능을 사용하여 데이터베이스 프로젝트를 개발하고 클라우드에 배포하기 전에 테스트할 수 있습니다.  
  
> [!WARNING]  
> SQL Server 개체 탐색기의 로컬 데이터베이스 노드 아래에 있는 데이터베이스는 해당하는 데이터베이스 프로젝트를 나타내는 것으로, 연결된 서버 인스턴스에 있는 동일한 이름의 데이터베이스와는 관련이 없습니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 활용합니다.  
  
### <a name="to-use-the-local-database"></a>로컬 데이터베이스를 사용하려면  
  
1.  **SQL Server 개체 탐색기**의 **SQL Server** 노드에는 **로컬**이라는 새 노드가 나타납니다. 이 노드가 로컬 데이터베이스 인스턴스입니다.  
  
2.  **로컬** 및 **데이터베이스** 노드를 확장합니다. TradeDev 프로젝트와 동일한 이름의 데이터베이스가 나타나는지 확인합니다. 이 데이터베이스 아래의 노드를 확장합니다. **Data Tools 작업** 창에서 **로컬** 노드의 모든 데이터베이스에 대한 진행률에 확장/가져오기 작업 상태가 표시됩니다. 해당 노드에는 이전 절차에서 만든 테이블 및 엔터티가 포함되어 있지 않습니다.  
  
3.  F5 키를 눌러 TradeDev 데이터베이스 프로젝트를 디버깅합니다.  
  
    기본적으로 SSDT에서는 데이터베이스 프로젝트를 디버깅하는 데 로컬 데이터베이스 서버를 사용합니다. 이 경우 SSDT에서는 먼저 프로젝트 빌드를 시도하고 오류가 없으면 프로젝트와 해당 엔터티를 로컬 데이터베이스에 배포합니다. 나중에 동일한 프로젝트를 디버깅하는 경우 SSDT에서는 마지막 디버깅 세션 이후 변경된 내용을 검색하고 변경 내용만 로컬 데이터베이스에 배포합니다.  
  
4.  **로컬** 데이터베이스 서버의 **TradeDev** 아래에 있는 노드를 다시 확장합니다. 이번에는 테이블, 뷰 및 함수가 로컬 데이터베이스 서버에 배포되었습니다.  
  
5.  **TradeDev** 노드를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
6.  스크립트 창에서 다음 코드를 붙여넣고 **쿼리 실행** 단추를 클릭하여 쿼리를 실행합니다.  
  
    ```  
    select * from dbo.GetProductsBySupplier(1)  
    ```  
  
7.  **메시지** 창에 ‘(0개 행이 영향을 받음)’이 표시되고, **결과** 창에 행이 반환되지 않습니다. 이는 실제 데이터가 실제로 포함되어 있는 연결된 데이터베이스 대신 로컬 데이터베이스에 대해 쿼리했기 때문입니다.  
  
    이 로컬 **TradeDev** 데이터베이스 아래의 **Products** 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택하여 이를 확인할 수 있습니다. 테이블이 비어 있는지 확인합니다.  
  
### <a name="to-replicate-real-data-to-the-local-database"></a>로컬 데이터베이스에 실제 데이터를 복제하려면  
  
1.  **SQL Server 개체 탐색기**에서 연결된 SQL Server 인스턴스를 확장하고 **TradeDev** 데이터베이스를 찾습니다.  
  
    **Suppliers** 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다.  
  
2.  데이터 편집기 위쪽의 **스크립트** 단추(오른쪽에서 두 번째 단추)를 클릭합니다. 스크립트의 `INSERT` 문을 복사합니다.  
  
3.  **로컬** 서버 인스턴스를 확장하고 **TradeDev** 노드를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
4.  이 쿼리 창에 `INSERT` 문을 붙여 넣고 쿼리를 실행합니다.  
  
5.  위의 단계를 반복하여 연결된 **TradeDev** 데이터베이스에 있는 **Products** 및 **Fruits** 테이블의 데이터를 로컬 **TradeDev** 데이터베이스에 복제합니다.  
  
6.  **로컬** 서버 인스턴스를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다. **데이터 보기**로 테이블을 검사하여 로컬 데이터베이스가 채워졌는지 확인합니다.  
  
7.  로컬 서버 인스턴스의 **TradeDev** 노드를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
8.  스크립트 창에서 다음 코드를 붙여넣고 **쿼리 실행** 단추를 클릭하여 쿼리를 실행합니다.  
  
    ```  
    select * from dbo.GetProductsBySupplier(1)  
    ```  
  
9. Transact**SQL 편집기 창 아래의** 결과\- 창에 `Products` 테이블의 Apples 및 Potato Chips 행이 반환됩니다.  
  
