---
title: 기록 특성 옵션(느린 변경 차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b40e52ec972607d2fd5345c5715c9faae3383f1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082726"
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>기록 특성 옵션(느린 변경 차원 마법사)
  **기록 특성 옵션** 대화 상자를 사용하여 시작 및 종료 날짜별로 기록 특성을 표시하거나 이 용도로 특별히 만든 열에 기록 특성을 기록할 수 있습니다.  
  
 이 마법사에 대한 자세한 내용은 [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **단일 열을 사용하여 현재 및 만료 레코드 표시**  
 단일 열을 사용하여 기록 특성의 상태를 기록하도록 선택한 경우 다음 옵션을 사용할 수 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**현재 레코드 표시 열**|현재 레코드를 표시할 열을 선택합니다.|  
|**현재 값**|**True** 또는 **현재** 를 사용하여 현재 레코드인지 여부를 표시할 수 있습니다.|  
|**만료 값**|**False** 또는 **만료됨** 을 사용하여 레코드가 기록 값인지 여부를 표시할 수 있습니다.|  
  
 **시작 및 종료 날짜를 사용하여 현재 및 만료 레코드 식별**  
 이 옵션의 차원 테이블에는 날짜 열이 포함되어 있어야 합니다. 시작 및 종료 날짜별로 기록 특성을 표시하도록 선택한 경우 다음 옵션을 사용할 수 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**시작 날짜 열**|시작 날짜를 포함할 차원 테이블의 열을 선택합니다.|  
|**종료 날짜 열**|종료 날짜를 포함할 차원 테이블의 열을 선택합니다.|  
|**날짜 값 설정 변수**|목록에서 날짜 변수를 선택합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [느린 변경 차원 마법사를 사용하여 출력 구성](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  