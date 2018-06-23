---
title: 매개 변수화 대화 상자 | Microsoft Docs
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
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9a8f684eb94884d14c433539d2a617485379a784
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187020"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  **매개 변수화** 대화 상자를 사용하여 새 매개 변수나 기존 매개 변수를 태스크의 속성과 연결할 수 있습니다. 태스크나 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 제어 흐름 탭을 마우스 오른쪽 단추로 클릭한 다음 **매개 변수화**를 클릭하여 이 대화 상자를 엽니다. 다음 목록에서는 이 대화 상자의 UI 요소에 대해 설명합니다. 매개 변수에 대한 자세한 내용은 [Integration Services&#40;SSIS&#41; 매개 변수](integration-services-ssis-package-and-project-parameters.md)를 참조하세요.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **속성**  
 매개 변수와 연결할 태스크의 속성을 선택합니다. 이 목록은 매개 변수화할 수 있는 모든 속성으로 채워집니다.  
  
 **기존 매개 변수 사용**  
 이 옵션을 선택하여 태스크의 속성을 기존 매개 변수와 연결한 다음 드롭다운 목록에서 매개 변수를 선택합니다.  
  
 **매개 변수 사용 안 함**  
 매개 변수에 대한 참조를 제거하려면 이 옵션을 선택합니다. 매개 변수는 삭제되지 않습니다.  
  
 **새 매개 변수 만들기**  
 이 옵션을 선택하여 태스크의 속성과 연결할 새 매개 변수를 만듭니다.  
  
 **이름**  
 만들려는 매개 변수의 이름을 지정합니다.  
  
 **설명**  
 매개 변수에 대한 설명을 지정합니다.  
  
 **Value**  
 매개 변수의 기본값을 지정합니다. 이 값은 디자인 기본값이라고도 하며 나중에 배포할 때 재정의할 수 있습니다.  
  
 **범위**  
 **프로젝트** 또는 **패키지** 옵션을 선택하여 매개 변수의 범위를 지정합니다. 프로젝트 매개 변수는 프로젝트가 수신하는 외부 입력을 프로젝트 내 하나 이상의 패키지에 제공하기 위해 사용됩니다. 패키지 매개 변수를 사용하면 패키지를 편집하여 다시 배포할 필요 없이 패키지 실행을 수정할 수 있습니다.  
  
 **구분**  
 확인란을 선택하거나 선택 취소하여 매개 변수가 중요한지 여부를 지정합니다. 구분 매개 변수 값은 카탈로그에서 암호화되고 Transact-SQL 또는 SQL Server Management Studio를 사용하여 볼 경우 NULL 값으로 나타납니다.  
  
 **필수**  
 매개 변수 사용 시 디자인 기본값 이외의 값을 지정해야 패키지를 실행할 수 있는지 여부를 지정합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
  