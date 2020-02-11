---
title: 경고 디자이너에서 데이터 경고 편집 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- editing, data alerts
- updating, data alerts
- editing, alerts
- updating, alerts
ms.assetid: dde3664d-90b5-4b12-969e-39152c86e58a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 948bf1fd8145da9db9d0e0b81beabb8e7b3efaf2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109246"
---
# <a name="edit-a-data-alert-in-alert-designer"></a>경고 디자이너에서 데이터 경고 편집
  데이터 경고 관리자에서 편집할 데이터 경고 정의를 엽니다. 경고 정의를 만든 사용자만 해당 정의를 편집할 수 있습니다. 데이터 경고 관리자를 여는 방법은 [데이터 경고 관리자에서 내 데이터 경고 관리](manage-my-data-alerts-in-data-alert-manager.md)를 참조하세요.  
  
 다음 그림은 데이터 경고 관리자에 있는 데이터 경고의 상황에 맞는 메뉴를 보여 줍니다.  
  
 ![편집을 클릭하여 데이터 경고 디자이너 열기](media/rs-alertmanageriwopendesigner.gif "편집을 클릭하여 데이터 경고 디자이너 열기")  
  
 다음 절차에는 데이터 경고 디자이너에서 편집할 경고 정의를 데이터 경고 관리자에서 열기 위한 단계가 포함되어 있습니다.  
  
### <a name="to-edit-a-data-alert-definition-in-data-alert-designer"></a>데이터 경고 디자이너에서 데이터 경고 정의를 편집하려면  
  
1.  데이터 경고 관리자에서 편집할 데이터 경고 정의를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.  
  
     경고 정의가 데이터 경고 디자이너에서 열립니다.  
  
2.  규칙, 일정 설정 및 전자 메일 설정을 업데이트합니다. 자세한 내용은 [데이터 경고 디자이너](../../2014/reporting-services/data-alert-designer.md) 및 [데이터 경고 디자이너에서 데이터 경고 만들기](create-a-data-alert-in-data-alert-designer.md)를 참조하세요.  
  
    > [!NOTE]  
    >  다른 데이터 피드를 선택할 수는 없습니다. 다른 데이터 피드를 사용하려면 새 데이터 경고 정의를 만들어야 합니다.  
  
3.  **저장**을 클릭합니다.  
  
    > [!NOTE]  
    >  보고서가 변경되고 보고서에서 생성된 데이터 피드가 변경된 경우 경고 정의가 더 이상 유효하지 않을 수 있습니다. 이러한 예로는 해당 규칙에서 경고 정의가 참조하는 열이 보고서에서 삭제되었거나 데이터 형식을 변경하는 경우 또는 보고서가 삭제 또는 이동되는 경우를 들 수 있습니다. 유효하지 않은 경고 정의를 열 수는 있지만 정의를 작성할 때 사용한 보고서 데이터 피드의 현재 버전을 기준으로 유효한 경고 정의만 다시 저장할 수 있습니다. 보고서에서 데이터 피드를 생성하는 방법은 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [경고 관리자를 위한 데이터 경고 관리자](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [Reporting Services 데이터 경고](../ssms/agent/alerts.md)  
  
  
