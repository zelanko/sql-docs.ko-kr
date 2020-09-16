---
description: 자체 조인 자동으로 만들기(Visual Database Tools)
title: 자체 조인 자동으로 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- self-joins
- joins [SQL Server], self
ms.assetid: f9ec90e8-3aad-415c-a5c4-8dfa9540e37f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 3792e29ae83d28e8c695cfebbd5fc086fe4c267b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468389"
---
# <a name="create-self-joins-automatically-visual-database-tools"></a>자체 조인 자동으로 만들기(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
데이터베이스에서 테이블에 반사 관계가 있는 경우 자동으로 자체 조인할 수 있습니다.  
  
### <a name="to-create-a-self-join-automatically"></a>자체 조인을 자동으로 만들려면  
  
1.  작업할 테이블을 [다이어그램 창](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 에 추가합니다.  
  
2.  다이어그램 창에 같은 테이블이 두 번 표시되도록 같은 테이블을 다시 추가합니다.  
  
    [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 는 테이블 이름에 일련 번호를 추가하여 두 번째 인스턴스에 별칭을 할당합니다. 또한 쿼리 및 뷰 디자이너는 테이블이 쿼리와 관련되는 서로 다른 두 가지 방식을 나타내는 조인 선을 두 개의 사각형 사이에 만듭니다.  
  
## <a name="see-also"></a>참고 항목  
[조인을 사용한 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
