---
title: '작업 4: 일치 작업의 결과를 Excel 파일로 내보내기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fd85a523804232deff14f2e1da5485229f943dd2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999660"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>태스크 4: 일치 작업의 결과를 Excel 파일로 내보내기
  이 작업에서는 일치 작업의 결과를 Excel 파일로 내보냅니다.

1.  **내보내기** 페이지에서 **대상 유형** 으로 **Excel 파일**을 선택합니다.

2.  **Survivorship 결과** 옵션을 선택합니다. survivorship 프로세스에서 DQS는 사용자가 선택한 **Survivorship 규칙** 에 따라 각 클러스터에 대해 Survivor 레코드를 결정합니다.

3.  **찾아보기** 를 클릭하고 출력 파일을 저장할 폴더로 이동합니다.

4.  이름을 **Cleansed and Matched Suppliers.xls** 로 입력하고 **열기**를 클릭합니다.

5.  **Survivorship 규칙** 에 대해 **피벗 레코드**가 선택되었는지 확인합니다. 이 옵션을 선택하면 각 클러스터의 피벗 레코드가 클러스터의 출력으로 선택됩니다. Survivorship 규칙의 다른 옵션은 다음과 같습니다.

    1.  **가장 완전한 레코드:** 채워진 필드가 가장 많은 레코드가 Survivor 레코드가 됩니다.

    2.  **가장 긴 레코드:** 원본 필드에서 용어 수가 가장 많은 레코드가 Survivor 레코드가 됩니다.

    3.  **가장 완전하고 가장 긴 레코드:** 채워진 필드가 가장 많고 각 필드의 용어 수가 가장 많은 레코드가 Survivor 레코드가 됩니다.

     ![일치하는 항목에서 결과 내보내기 페이지](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "일치하는 항목에서 결과 내보내기 페이지")

6.  **내보내기** 를 클릭하여 결과를 Excel 파일로 내보냅니다.

7.  **닫기** 를 클릭하여 **일치하는 항목 내보내기** 대화 상자를 닫습니다.

8.  **마침** 을 클릭하여 일치 작업을 마칩니다.

9. **Cleansed and Matched Suppliers.xlsx** 파일을 열고 중복 항목이 없는지 확인합니다(SupplierID).

 이제 중복 항목 제거를 위해 정리 및 일치 작업이 수행된 공급자 데이터가 준비되었습니다.

## <a name="next-step"></a>다음 단계
 [4단원: MDS에 공급자 데이터 저장](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)


