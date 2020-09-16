---
description: 한 데이터베이스 다이어그램에서 다른 다이어그램으로 테이블 복사(Visual Database Tools)
title: 한 데이터베이스 다이어그램에서 다른 다이어그램으로 테이블 복사
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- duplicating tables
ms.assetid: 155a4f09-9321-4887-a7d4-aa2ce6b51277
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b75d0d2c3429f5649e1034ea9eb4f922ca995652
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468486"
---
# <a name="copy-tables-from-one-database-diagrams-to-another-visual-database-tools"></a>한 데이터베이스 다이어그램에서 다른 다이어그램으로 테이블 복사(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
같은 데이터베이스의 한 데이터베이스 다이어그램에서 다른 데이터베이스 다이어그램으로 테이블을 복사할 수 있습니다.  
  
한 데이터베이스 다이어그램에서 다른 다이어그램으로 테이블을 복사하면 다른 다이어그램에는 그 테이블에 대한 참조만 추가되며 데이터베이스에 테이블이 복제되는 것은 아닙니다. 예를 들어 한 데이터베이스 다이어그램에서 다른 다이어그램으로 `authors` 테이블을 복사하면 각 다이어그램은 데이터베이스에 있는 같은 `authors` 테이블을 참조하게 됩니다.  
  
### <a name="to-copy-a-table-from-another-database-diagram"></a>다른 데이터베이스 다이어그램으로부터 테이블을 복사하려면  
  
1.  복사할 테이블이 있는 데이터베이스에 연결되어 있는지 확인합니다.  
  
2.  원본 및 대상 데이터베이스 다이어그램을 열고 원본 다이어그램에서 대상 다이어그램으로 복사할 테이블을 선택합니다.  
  
3.  도구 모음의 **복사** 단추를 클릭합니다. 이 단추를 클릭하면 선택한 테이블 정의가 클립보드에 복사됩니다.  
  
4.  대상 다이어그램으로 전환합니다. 이 다이어그램은 원본 다이어그램과 같은 데이터베이스에 있어야 합니다.  
  
5.  도구 모음에 있는 **붙여넣기** 단추를 클릭합니다. 클립보드 내용이 새 위치에 나타나고 다른 위치를 클릭할 때까지 강조 표시됩니다. 대상 다이어그램에서 선택한 테이블과 다른 테이블 사이에 관계가 있으면 관계 선이 자동으로 그려집니다.  
  
어느 한 쪽 다이어그램에서 테이블을 편집하면 변경 내용은 두 다이어그램에 모두 반영됩니다. 마찬가지로 어느 한 쪽 다이어그램에서 테이블을 저장하면 해당 테이블은 더 이상 두 다이어그램 모두에서 "수정"된 것으로 간주되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 다이어그램 작업&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[다이어그램에 테이블 추가&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
