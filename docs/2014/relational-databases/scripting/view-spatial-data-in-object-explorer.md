---
title: 개체 탐색기에서 공간 데이터 보기
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5ac09bdbc05f406d8d7925af1c9a45346913151
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75242951"
---
# <a name="view-spatial-data-in-object-explorer"></a>개체 탐색기에서 공간 데이터 보기
  쿼리 편집기의 **공간 데이터 결과** 창에서는 **결과** 창에 표 형식으로 표시 되는 데이터 외에도 공간 데이터 결과를 볼 수 있는 시각적 매핑 도구를 제공 합니다. 
  **공간 데이터 결과** 창에 공간 데이터를 표시하려면 쿼리 결과에서 기하 도형 또는 지리 데이터가 포함된 적어도 하나 이상의 공간 데이터 열이 있어야 합니다.  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>공간 데이터 결과 창에서 공간 데이터를 보려면  
  
1.  쿼리 편집기에서 **공간 데이터 결과** 탭을 클릭합니다.  
  
    > [!NOTE]  
    >  쿼리 결과에 공간 데이터가 포함되어 있지 않거나 결과가 텍스트로 반환되도록 지정한 경우에는 이 창을 사용할 수 없습니다.  
  
2.  
  **공간 열 선택** 목록에서 보려는 열을 선택합니다. 테이블에 공간 열이 하나만 있는 경우 이 열이 목록의 기본 옵션입니다.  
  
3.  
  **레이블 열 선택** 목록에서 데이터 레이블로 사용할 공간이 아닌 열을 선택합니다.  
  
4.  
  **투영 선택** 목록에서 지리 데이터에 사용할 투영 모드를 선택합니다. 기본 투영 모드는 Equirectangular이며 Mercator, Robinson 또는 Bonne도 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  공간 열에 기 하 도형 데이터가 포함 되어 있으면 **프로젝션을 선택할** 수 없습니다.  
  
5.  
  **확대/축소** 슬라이더를 조정하여 매핑된 요소의 시각적 크기를 늘립니다. 다각형 모양의 경우 레이블 텍스트를 넣을 수 있을 만큼 큰 경우에만 레이블이 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [공간 결과 창](spatial-results-window.md)   
 [데이터베이스 엔진 쿼리 편집기 &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)   
 [쿼리 및 텍스트 편집기 &#40;SQL Server Management Studio&#41;](query-and-text-editors-sql-server-management-studio.md)  
  
  
