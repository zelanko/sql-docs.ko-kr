---
title: '방법: 테이블 디자이너를 사용하여 테이블 및 관계 관리 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.columnspecification.index.dialog
- sql.data.tools.design.table.columnsgrid.view
- sql.data.tools.design.table.scriptpanel
ms.assetid: 322a2903-d7a6-4f52-9048-1bd413b4c799
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1d70fe813437ff6204173dc20df90d029f6568fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65096860"
---
# <a name="how-to-use-the-table-designer-to-manage-tables-and-relationships"></a>방법: 테이블 디자이너를 사용하여 테이블 및 관계 관리
테이블 디자이너에서는 Transact\-SQL 편집기와 함께 테이블 관련 프로그래밍 개체를 포함하여 SQL Server 데이터베이스의 테이블 구조를 만들고 편집하기 위한 시각적 환경을 제공합니다.  연결된 데이터베이스 또는 프로젝트의 새 테이블을 만들거나 SQL Server 개체 탐색기 또는 솔루션 탐색기에서 테이블을 편집하기 위해 두 번 클릭하면 테이블 디자이너가 시작됩니다.  
  
이 디자이너는 열 표, 스크립트 창 및 컨텍스트 창으로 구성되어 있습니다. 열 표에는 테이블의 모든 열이 나열됩니다. 이 표에서 열을 추가, 편집 및 삭제할 수 있습니다.  컨텍스트 창에는 키, 인덱스, 제약 조건, 트리거 등의 테이블 정의에 대한 논리 뷰가 제공되며, 이 창에서 개체를 선택하여 개별 열과의 관계를 강조 표시할 수 있습니다. 이 창에서 테이블에 새 개체를 추가하고 속성 표에서 선택한 개체의 속성을 편집할 수도 있습니다. 스크립트 창에는 테이블 구조의 정의가 표시되고, 컨텍스트 창 또는 열 표에서 선택한 개체의 스크립트가 강조 표시됩니다. 뷰에 열 표와 컨텍스트 창을 함께 표시하고 스크립트를 편집할 수 있습니다. 세 창 중 하나에서 변경한 내용은 즉시 다른 두 창에 전파됩니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 절차에서 만들어진 엔터티를 사용합니다.  
  
### <a name="to-create-a-new-table"></a>새 테이블을 만들려면  
  
1.  이전 절차에서 작업한 TradeDev 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 **dbo** 폴더를 확장하고 **테이블** 폴더를 마우스 오른쪽 단추로 클릭한 후 **추가**를 선택하고 **테이블**을 선택합니다.  
  
3.  새 테이블의 이름을 **Shipper**로 지정하고 **추가**를 클릭합니다.  
  
4.  테이블 디자이너가 열립니다. 열 표에서 이름과 데이터 형식이 각각 **ShipperName** 및 **int**인 새 열을 테이블에 추가합니다.  
  
5.  **속성** 창에서 열의 속성을 편집할 수도 있습니다. **ShipperName** 열을 클릭하고 **속성** 창에서 이 열의 **DataType** 및 **length**를 각각 **nvarchar** 및 **128**로 변경합니다. 포커스를 필드 외부로 이동하면 디자이너의 스크립트 창과 열 표가 자동으로 업데이트되어 변경 내용이 반영됩니다.  
  
### <a name="to-create-a-new-foreign-key-constraint"></a>새 외래 키 제약 조건을 만들려면  
  
1.  디자이너의 컨텍스트 창에서 **외래 키** 노드를 마우스 오른쪽 단추로 클릭하고 **새 외래 키 추가**를 선택합니다.  
  
2.  노드 수는 자동으로 1씩 증가합니다. Enter 키를 눌러 제약 조건의 기본 이름을 그대로 사용합니다.  
  
3.  스크립트 창에서 제약 조건의 기본 정의를 다음과 같이 바꿉니다.  
  
    ```  
    CONSTRAINT [FK_Shipper_Products] FOREIGN KEY ([Id]) REFERENCES [dbo].[Products]([Id])  
    ```  
  
    오프라인 프로젝트의 데이터베이스 엔터티를 만들고 편집하는 방법은 연결된 데이터베이스에 대해 작업을 수행할 때와 동일합니다.  
  
## <a name="see-also"></a>참고 항목  
[방법: 테이블 디자이너를 사용하여 데이터베이스 개체 만들기](../ssdt/how-to-create-database-objects-using-table-designer.md)  
  
