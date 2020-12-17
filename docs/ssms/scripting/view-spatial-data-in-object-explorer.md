---
title: 개체 탐색기에서 공간 데이터 보기
description: 쿼리 편집기 공간 데이터 결과 창의 시각적 매핑 도구를 사용하여 공간 데이터 결과(기하학적 또는 지리적)를 보는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ca0cfe4e93efb41bf49f2744da0968e0deebf284
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480574"
---
# <a name="view-spatial-data-in-object-explorer"></a>개체 탐색기에서 공간 데이터 보기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  쿼리 편집기의 **공간 데이터 결과** 창은 공간 데이터 결과와 **결과** 창에 표 형식으로 표시되는 데이터를 볼 수 있는 시각적인 매핑 도구를 제공합니다. **공간 데이터 결과** 창에 공간 데이터를 표시하려면 쿼리 결과에서 기하 도형 또는 지리 데이터가 포함된 적어도 하나 이상의 공간 데이터 열이 있어야 합니다.  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>공간 데이터 결과 창에서 공간 데이터를 보려면  
  
1.  쿼리 편집기에서 **공간 데이터 결과** 탭을 클릭합니다.  
  
    > [!NOTE]  
    >  쿼리 결과에 공간 데이터가 포함되어 있지 않거나 결과가 텍스트로 반환되도록 지정한 경우에는 이 창을 사용할 수 없습니다.  
  
2.  **공간 열 선택** 목록에서 보려는 열을 선택합니다. 테이블에 공간 열이 하나만 있는 경우 이 열이 목록의 기본 옵션입니다.  
  
3.  **레이블 열 선택** 목록에서 데이터 레이블로 사용할 공간이 아닌 열을 선택합니다.  
  
4.  **투영 선택** 목록에서 지리 데이터에 사용할 투영 모드를 선택합니다. 기본 투영 모드는 Equirectangular이며 Mercator, Robinson 또는 Bonne도 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  공간 열에 기하 도형 데이터가 포함되어 있지 않으면 **투영 선택** 을 사용할 수 없습니다.  
  
5.  **확대/축소** 슬라이더를 조정하여 매핑된 요소의 시각적 크기를 늘립니다. 다각형 모양의 경우 레이블 텍스트를 넣을 수 있을 만큼 큰 경우에만 레이블이 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터 결과 창](./spatial-results-window.md)   
 [데이터베이스 엔진 쿼리 편집기&#40;SQL Server Management Studio&#41;](../f1-help/database-engine-query-editor-sql-server-management-studio.md)   
 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../f1-help/database-engine-query-editor-sql-server-management-studio.md?view=sql-server-ver15)  
  
