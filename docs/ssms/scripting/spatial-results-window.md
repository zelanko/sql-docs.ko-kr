---
title: 공간 데이터 결과 창
description: 공간 데이터를 보기 위한 시각적 매핑 도구를 제공하는 공간 결과 창을 사용하는 방법을 알아봅니다. 공간 데이터 결과를 보려면 쿼리 결과에 기하 도형 또는 지리 데이터가 포함된 공간 열이 있어야 합니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c2d5a477-6496-4d01-adee-7322ebdfadf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3ed7e6dadeacc6ede7b5ee053a61977ed27c1174
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036339"
---
# <a name="spatial-results-window"></a>공간 데이터 결과 창
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  **공간 데이터 결과** 창에서는 공간 데이터를 볼 수 있는 시각적인 매핑 도구를 제공합니다. 공간 데이터 결과를 보려면 쿼리 결과에 기하 도형 또는 지리 데이터가 포함된 공간 열이 있어야 합니다.  
  
> [!NOTE]  
>  **공간 데이터 결과** 창은 결과가 **결과** 창에 표 형식으로 반환되는 경우에만 사용할 수 있습니다. 결과가 텍스트로 반환되도록 지정한 경우에는 이 창을 사용할 수 없습니다.  
  
## <a name="options"></a>옵션  
 **공간 열 선택**  
 쿼리 결과의 공간 열 중에서 보려는 공간 열을 지정합니다. 열은 한 번에 하나씩만 선택할 수 있습니다.  
  
 **레이블 열 선택**  
 쿼리 결과에 반환된 열 중에서 공간이 아닌 열을 지정하여 공간 데이터에 레이블을 지정합니다. 열은 한 번에 하나씩만 선택할 수 있습니다.  
  
 쿼리로 점만 반환된 경우 이 옵션을 사용할 수 없습니다.  
  
 **투영 선택**  
 Equirectangular, Mercator, Robinson 또는 Bonne 투영 모드 중 하나로 지리 데이터를 표시합니다.  
  
 기하 도형 데이터에 대해서는 이 옵션을 사용할 수 없습니다.  
  
 **Zoom**  
 맵 표시를 지수 배율로 조정합니다.  
  
 **눈금선 표시**  
 좌표 눈금선 표시를 설정하거나 해제합니다.  
  
 다각형 모양의 경우 레이블 텍스트를 넣을 수 있을 만큼 큰 경우에만 레이블이 표시됩니다. 작은 모양에 레이블을 표시하려면 확대/축소를 조정하십시오.  
  
> [!NOTE]  
>  점에는 레이블을 지정할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [개체 탐색기에서 공간 데이터 보기](./view-spatial-data-in-object-explorer.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [데이터베이스 엔진 쿼리 편집기&#40;SQL Server Management Studio&#41;](../f1-help/database-engine-query-editor-sql-server-management-studio.md)   
 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../f1-help/database-engine-query-editor-sql-server-management-studio.md?view=sql-server-ver15)  
  
