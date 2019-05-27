---
title: 새 모델 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 27d5bf66-b0e7-489e-a830-ffe2ec8e5350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5b9fdcac2499cdf33d98ba636596218c14704f9d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108206"
---
# <a name="new-model-page-report-manager"></a>새 모델 페이지(보고서 관리자)
  이 페이지를 사용하여 공유 데이터 원본에서 기본 보고서 모델을 생성할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 다차원 데이터 원본, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관계형 데이터 원본, 그리고 Oracle 관계형 데이터 원본에서만 보고서 모델을 생성할 수 있습니다.  
  
 보고서 관리자에서 생성하는 모델은 공유 데이터 원본의 스키마를 기반으로 합니다. 엔터티, 폴더 및 필드는 데이터 원본의 모든 테이블 및 열에 대해 생성됩니다. 항목을 제외할 수 없으며, 모델이 생성되는 방법을 결정하는 옵션도 설정할 수 없습니다. 모델을 사용자 지정하거나 구체화하려면 모델 디자이너를 사용해야 합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-new-model-page"></a>새 모델 페이지를 열려면  
  
1.  보고서 관리자를 열고 모델을 생성하려는 공유 데이터 원본을 찾습니다.  
  
2.  데이터 원본 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 다음 단계 중 하나를 수행하십시오.  
  
    -   **보고서 모델 생성** 을 클릭하여 새 모델 페이지를 엽니다.  
  
    -   **관리** 를 클릭하여 보고서의 일반 속성 페이지를 연 다음 **모델 생성** 을 클릭하여 새 모델 페이지를 엽니다.  
  
## <a name="options"></a>변수  
 **이름**  
 모델의 이름을 지정합니다. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 이름 지정 시에는 다음 문자를 사용하지 마십시오.  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **설명**  
 모델에 대한 설명을 표시합니다. 보고서 관리자를 통해 이 항목을 보는 사용자는 폴더 계층을 검색할 때 이 설명을 볼 수 있습니다.  
  
 **위치 변경**  
 새 모델의 폴더 위치를 표시합니다. **위치 변경** 단추를 클릭하여 다른 위치를 선택할 수 있습니다.  
  
  
