---
description: 데이터베이스 테이블 생성 및 업데이트
title: 테이블 만들기 및 업데이트
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Visual Database Tools [SQL Server], Table Designer
- Table Designer, designing tables
- opening tables
- opening Table Designer
- tables [SQL Server], opening
- Table Designer, opening
ms.assetid: c49e0155-5dcb-481f-9538-e1bde77105e2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/25/2017
ms.openlocfilehash: 5a0bbc50ddef7baa1cd2f21211f692703f41b251
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491706"
---
# <a name="create-and-update-database-tables"></a>데이터베이스 테이블 생성 및 업데이트

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

테이블 디자이너는 [데이터베이스 테이블](../../relational-databases/tables/tables.md)을 디자인하고 시각화하는 데 시용하는 시각적 도구입니다. SSMS(SQL Server Management Studio) 테이블 디자이너를 사용하여 테이블, 열, 키, 인덱스, 관계, 제약 조건 등을 만들거나 편집하거나 삭제합니다.  

## <a name="create-a-table"></a>테이블 만들기

1. 데이터베이스에서 **테이블** 노드를 마우스 오른쪽 단추로 클릭하고 **새** > **테이블**을 선택합니다.

    ![새 테이블](../media/design-tables/new-table.png)

2. 테이블에 [열](column-properties-visual-database-tools.md)을 추가합니다.

    ![테이블 디자인](../media/design-tables/new-table2.png)

3. 디자이너를 닫고 변경 내용을 저장합니다.

## <a name="update-a-table"></a>테이블 업데이트

1. 데이터베이스의 **테이블** 노드 아래 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.

    ![테이블 업데이트](../media/design-tables/update-table.png)

2. 원하는 테이블 설정을 업데이트합니다.

    ![테이블 만들기](../media/design-tables/update-table2.png)

3. 디자이너를 닫고 변경 내용을 저장합니다.

## <a name="see-also"></a>참고 항목

- [테이블](../../relational-databases/tables/tables.md)
- [테이블 속성&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/table-properties-visual-database-tools.md)
- [열 속성](column-properties-visual-database-tools.md)
- [테이블에 열 추가](../../relational-databases/tables/add-columns-to-a-table-database-engine.md)
- [기본 및 외래 키](../../relational-databases/tables/primary-and-foreign-key-constraints.md)
- [인덱스](../../relational-databases/indexes/indexes.md)
- [데이터 형식(Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
- [SSMS(SQL Server Management Studio) 다운로드](../download-sql-server-management-studio-ssms.md)
- [데이터베이스 만들기 및 Visual Studio에서 테이블 추가](/visualstudio/data-tools/create-a-sql-database-by-using-a-designer)
