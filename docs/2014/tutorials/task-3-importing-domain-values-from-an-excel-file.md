---
title: '태스크 3: Excel 파일에서 도메인 값 가져오기 | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: fd5f73f95dce1d40689062a368e1cc222023541c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078943"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>태스크 3: Excel 파일에서 도메인 값 가져오기
  이 작업에서는 Excel 파일의 워크시트에서 **State** 도메인에 대한 값을 가져옵니다.  
  
1.  **도메인 목록** 에서 **State**도메인을 클릭합니다.  
  
2.  **도메인 값** 탭이 오른쪽 창에 활성화되어 있는지 확인합니다.  
  
3.  오른쪽 창의 도구 모음에서 **값 가져오기** 단추 옆에 있는 **아래쪽 화살표** 를 클릭하고 **Excel에서 유효한 값 가져오기**를 클릭합니다.  
  
     ![Excel 메뉴에서 유효한 값 가져오기](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "Excel 메뉴에서 유효한 값 가져오기")  
  
4.  **찾아보기**를 클릭하고 **Suppliers.xls**를 선택한 후 **열기**를 클릭합니다.  
  
5.  **워크시트** 에 대해 **StatesToImport$** 를 선택합니다.  
  
     ![도메인 가져오기 값 대화 상자](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "도메인 가져오기 값 대화 상자")  
  
6.  **확인** 을 클릭하여 **도메인 값 가져오기** 대화 상자를 닫습니다. 가져온 모든 State 이름이 목록에 표시됩니다. 가져온 후에는 **새 항목만 표시** 옵션이 자동으로 선택됩니다. 값을 가져올 때 이전 값이 목록에 없으면 가져오기 후 이 옵션이 자동으로 설정되었기 때문입니다. 모든 값을 표시하려면 확인란의 선택을 취소합니다. 동일한 값 집합을 다시 가져올 경우, 도메인에 이미 있는 값은 가져오기가 다시 수행되지 않습니다.  
  
     ![도메인 값에 새 확인란만 표시](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "도메인 값에 새 확인란만 표시")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 4: 도메인 규칙 설정](../../2014/tutorials/task-4-setting-domain-rules.md)  
  
  