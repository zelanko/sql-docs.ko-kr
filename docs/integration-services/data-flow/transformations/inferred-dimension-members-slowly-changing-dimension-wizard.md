---
title: "유추 차원 멤버 (느린 변경 차원 마법사) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b99116c19f5ec69fcf382069a1ca3c76ee65b3d6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>유추 차원 멤버(느린 변경 차원 마법사)
  **유추 차원 멤버** 대화 상자를 사용하여 유추 멤버를 사용하기 위한 옵션을 지정할 수 있습니다. 유추 멤버는 팩트 테이블이 아직 로드되지 않은 차원 멤버를 참조할 때 존재합니다. 유추 멤버에 대한 데이터가 로드되면 새 레코드를 만드는 대신 기존 레코드를 업데이트할 수 있습니다.  
  
 이 마법사에 대한 자세한 내용은 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)를 참조하십시오.  
  
## <a name="options"></a>옵션  
 **유추 멤버 지원 사용**  
 유추 멤버를 사용하도록 선택한 경우 다음 두 옵션 중 하나를 선택해야 합니다.  
  
 **변경 유형을 가진 열은 모두 Null임**  
 새 유추 멤버 레코드에서 변경 유형을 가진 모든 열에 Null 값을 입력할지 여부를 지정합니다.  
  
 **부울 열을 사용하여 현재 레코드가 유추 멤버인지 여부 표시**  
 기존 부울 열을 사용하여 현재 레코드가 유추 멤버인지 여부를 나타낼지 여부를 지정합니다.  
  
 **유추 멤버 표시**  
 위에서 설명한 것처럼 부울 열을 사용하여 유추 멤버를 나타내도록 선택한 경우 목록에서 열을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [느린 변경 차원 마법사를 사용 하 여 출력 구성](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
