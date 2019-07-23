---
title: CDC 분할자 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 40f9fd60bcfd5e25f841d0cda05089da5f73e268
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045366"
---
# <a name="cdc-splitter"></a>CDC 분할자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC 분할자는 CDC 원본 데이터 흐름의 단일 변경 행 흐름을 삽입, 업데이트 및 삭제 작업을 위한 여러 데이터 흐름으로 분할합니다. 데이터 흐름은 필요한 열인 `__$operation` 과 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 변경 테이블의 해당 표준 값을 기반으로 분할됩니다.  
  
|작업 값|출력|설명|  
|------------------------|------------|-----------------|  
|1|DELETE|삭제된 행|  
|2|Insert|삽입된 행( **병합을 사용한 순 변경 내용** CDC 모드를 사용하는 경우에는 제공되지 않음)|  
|3|Update|업데이트 전 행( **이전 값이 포함된 모두** CDC 모드를 사용하는 경우에만 제공됨)|  
|4|Update|업데이트 후 행(업데이트 전을 따름)|  
|5|Update|병합 행( **병합을 사용한 순 변경 내용** CDC 모드를 사용하는 경우에만 제공됨)|  
|기타|Error||  
  
 분할자를 사용하여 미리 정의된 삽입, 삭제 및 업데이트 출력에 연결하여 해당 출력을 추가적으로 처리할 수 있습니다.  
  
 CDC 분할자 변환에 하나의 일반 입력과 하나의 오류 출력이 있습니다.  
  
## <a name="error-handling"></a>오류 처리  
 CDC 분할자 변환에 하나의 오류 출력이 있습니다. $operation 열의 잘못된 값이 포함된 입력 행은 잘못된 것으로 간주되며 입력의 **ErrorRowDisposition** 속성에 따라 처리됩니다.  
  
 구성 요소 오류 출력에 다음과 같은 출력 열이 포함됩니다.  
  
-   **오류 코드**: 1로 설정됩니다.  
  
-   **오류 열**: 오류의 원인이 되는 원본 열입니다(변환 오류의 경우).  
  
-   **오류 행 열**: 오류를 유발한 행의 입력 열입니다.  
  
## <a name="configuring-the-cdc-splitter"></a>CDC 분할자 구성  
 CDC 분할자에 대해 구성 가능한 속성은 없습니다.  
  
 CDC 분할자 사용에 대한 자세한 내용은 Microsoft SQL Server Integration Services용 CDC 구성 요소를 참조하십시오.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.  
  
 **고급 편집기** 대화 상자를 열려면  
  
-   **프로젝트의** 데이터 흐름 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 화면에서 CDC 분할자를 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [변경 유형에 따라 CDC 스트림 전송](../../integration-services/data-flow/direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
