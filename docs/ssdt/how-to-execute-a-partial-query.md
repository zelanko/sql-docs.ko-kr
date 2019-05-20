---
title: '방법: 부분 쿼리 실행 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: af04ab37-6cbb-4185-9382-e5922fa5b1df
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0dff2087286035b078f59ac1673a733fb3cc8358
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090173"
---
# <a name="how-to-execute-a-partial-query"></a>방법: 부분 쿼리 실행
Transact\-SQL 편집기에서는 스크립트의 특정 세그먼트를 강조 표시하고 해당 세그먼트를 단일 쿼리로 실행할 수 있습니다. 이렇게 하면 복잡한 쿼리의 섹션을 간단하게 디버깅할 수 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 사용합니다.  
  
### <a name="to-partially-execute-a-query"></a>쿼리를 부분적으로 실행하려면  
  
1.  **SQL Server 개체 탐색기**에서 **뷰** 아래의 **PerishableFruits**를 두 번 클릭하여 이 뷰를 Transact\-SQL 편집기에서 엽니다.  
  
2.  코드의 `SELECT p.Id, p.Name FROM dbo.Product p` 세그먼트를 강조 표시하고 마우스 오른쪽 단추를 클릭하고 **쿼리 실행**을 선택합니다.  
  
3.  `Products` 테이블에서 지정된 필드가 있는 모든 행이 **결과** 창에 반환됩니다.  
  
