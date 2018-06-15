---
title: 정책 평가 대화 상자, 정책 선택 페이지 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a92afcb9fec91f099b9ffbee048d5d2f2df884e2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32954048"
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>정책 평가 대화 상자, 정책 선택 페이지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 대화 상자를 사용하여 정책 기반 관리 정책을 평가합니다. **평가 결과** 페이지를 선택하면 정책을 준수하지 않는 대상 집합의 항목에 정책을 적용할 수 있습니다.  
  
## <a name="options"></a>변수  
 **원본**  
 정책의 원본을 지정합니다. 원본을 변경하려면 찾아보기 단추 (**...**)를 클릭하여 **원본 선택** 대화 상자를 엽니다.  
  
 **파일**  
 정책 기반 관리 정책이 포함된 파일의 경로를 입력하거나 찾아보기 단추(**...**)를 사용하여 파일을 선택합니다.  
  
 **Server**  
 원하는 정책이 포함된 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결하려면 선택합니다.  
  
 **정책: 정책**  
 지정된 정책에 대한 정책 대화 상자를 열려면 클릭합니다.  
  
 **정책: 범주**  
 정책의 범주입니다. 이 부분은 읽기 전용입니다.  
  
 **정책: 패싯**  
 정책에 의해 구현되는 패싯입니다. 이 부분은 읽기 전용입니다.  
  
 **평가**  
 평가 모드에서 정책을 실행합니다. 이렇게 하면 대상 집합에 대한 준수 보고서가 생성되지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다시 구성되거나 앞으로 정책이 준수되도록 하지는 않습니다.  
  
## <a name="possible-errors"></a>가능한 오류  
  
-   **대상이 없습니다.**  
  
     다음 이유 중 하나로 인해 대상 집합이 비어 있을 수 있습니다.  
  
    -   정책으로 지정된 유형의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대상이 없습니다.  
  
    -   서버 제한으로 인해 대상이 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 제외되었을 수 있습니다.  
  
    -   정책이 데이터베이스의 개체(예: 테이블, 뷰 또는 사용자)에 있는 경우 데이터베이스는 정책의 범주를 구독하지 않을 수 있습니다.  
  
    -   대상 집합 필터로 인해 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 대상이 제외되었을 수 있습니다.  
  
    -   대상 서버 유형은 정책을 평가하는 서버 유형과 다릅니다. 예를 들어 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대해 만든 정책을 평가하면 빈 대상 집합을 받게 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 평가 대화 상자, 평가 결과 페이지](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
