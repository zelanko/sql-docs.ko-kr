---
title: 템플릿 열기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dd59b435c1c0fbd3461333305824aca61c68d296
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245686"
---
# <a name="open-a-template"></a>템플릿 열기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
템플릿 탐색기에서 템플릿을 열 수 있습니다.  
  
## <a name="to-open-a-template-from-template-explorer"></a>템플릿 탐색기에서 템플릿을 열려면  
템플릿 탐색기에서 템플릿을 열 수 있습니다.  
  
1.  템플릿 탐색기를 열려면 **보기** 메뉴에서 **템플릿 탐색기**를 클릭합니다.  
  
2.  템플릿 범주 목록에서 열려는 템플릿이 포함된 범주를 확장합니다.  
  
3.  다음 세 가지 방법으로 템플릿을 엽니다.  
  
    1.  코드 편집기 창에서 열려는 템플릿을 두 번 클릭합니다.  
  
    2.  템플릿을 마우스 오른쪽 단추로 클릭하고 **열기** 를 선택하여 코드 편집기 창에서 템플릿을 엽니다.  
  
    3.  템플릿을 코드 편집기 창으로 끌어 편집기 창의 내용에 템플릿 코드를 추가합니다.  
  
템플릿을 연 후 **템플릿 매개 변수 바꾸기** 대화 상자에서 템플릿 매개 변수를 원하는 값으로 바꿀 수 있습니다.  
  
새 편집기 창에서 템플릿을 열 경우 현재 활성 연결의 자격 증명을 사용하여 창이 열립니다. 예를 들어 개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 인스턴스에 포커스가 있는 상태에서 CREATE DATABASE 템플릿을 열면 새 편집기 창은 해당 인스턴스에 대한 연결을 사용하여 열립니다. 활성 연결이 없는 경우에는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 로그인 대화 상자가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
[템플릿 탐색기](../../ssms/template/template-explorer.md)  
[템플릿 매개 변수 바꾸기](../../ssms/template/replace-template-parameters.md)  
  
