---
title: 템플릿 매개 변수 바꾸기 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7f81fcd7ad4f1ff8b99eccdaa2d3f1b0a0179e2e
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102654"
---
# <a name="replace-template-parameters"></a>템플릿 매개 변수 바꾸기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
템플릿에는 템플릿이 사용될 때마다 구현별 값으로 바꿀 수 있는 매개 변수가 포함되어 있습니다. 코드 편집기에서 템플릿을 연 후 매개 변수를 구현과 관련된 값으로 바꿀 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
**템플릿 매개 변수 값 지정** 대화 상자는 세 개의 열이 있는 표입니다. **매개 변수** 및 **형식** 열은 읽기 전용이므로 변경할 수 없습니다. **값** 열의 내용을 검토하고 기본값을 구현에 적절한 값으로 변경합니다.  
  
이 대화 상자를 사용하려면 스크립트의 매개 변수를 꺾쇠 괄호(`< >`)로 묶어 `<`*parameter_name*`,` *data_type*`,` *default_value*`>`형식으로 표시해야 합니다.  
  
## <a name="replace-template-parameters"></a>템플릿 매개 변수 바꾸기  
코드 편집기 창에서 템플릿을 연 후 다음 작업을 수행합니다.  
  
1.  **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정**을 클릭합니다.  
  
2.  **템플릿 매개 변수 값 지정** 대화 상자의 **값** 열에는 각 매개 변수에 대해 권장되는 값이 포함되어 있습니다. 이 값을 그대로 사용하거나 새 값으로 바꿉니다.  
  
3.  **확인** 을 클릭하여 **템플릿 매개 변수 바꾸기** 대화 상자를 닫고 쿼리 편집기에서 스크립트를 수정합니다.  
  
## <a name="see-also"></a>참고 항목  
[템플릿 탐색기](../../ssms/template/template-explorer.md)  
[템플릿 열기](../../ssms/template/open-a-template.md)  
  
