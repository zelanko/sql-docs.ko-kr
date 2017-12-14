---
title: "열 유형 제안 대화 상자 UI 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 78a2fb3483b72ff06582b8be30be2f937b2d1317
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>열 유형 제안 대화 상자 UI 참조
  **열 유형 제안** 대화 상자를 사용하여 파일 내용의 샘플링을 기반으로 플랫 파일 연결 관리자에 있는 열의 데이터 형식과 길이를 식별할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 사용하는 데이터 형식에 대한 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **행 수**  
 알고리즘에서 사용하는 샘플의 행 수를 입력하거나 선택합니다.  
  
 **가장 작은 정수 데이터 형식 제안**  
 평가를 건너뛰려면 이 확인란의 선택을 취소합니다. 이 확인란이 선택되어 있으면 정수 데이터를 포함하는 열에 대해 가능한 가장 작은 정수 데이터 형식을 확인합니다.  
  
 **가장 작은 실수 데이터 형식 제안**  
 평가를 건너뛰려면 이 확인란의 선택을 취소합니다. 이 확인란이 선택되어 있으면 실수 데이터를 포함하는 열에서 보다 작은 실수 데이터 형식인 DT_R4를 사용할 수 있는지 여부를 확인합니다.  
  
 **다음 값을 사용하여 부울 열 식별**  
 부울 값 True와 False로 사용할 값 두 개를 입력합니다. 쉼표로 값을 구분해야 하며 첫 번째 값이 True를 나타냅니다.  
  
 **문자열 열 패딩**  
 문자열 패딩을 사용하려면 이 확인란을 선택합니다.  
  
 **패딩 비율**  
 문자 데이터 형식 열의 길이에 추가할 열 길이의 비율을 입력하거나 선택합니다. 비율은 정수여야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [플랫 파일 연결 관리자](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
