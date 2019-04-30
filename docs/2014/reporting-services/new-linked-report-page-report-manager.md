---
title: 새 링크 된 보고서 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: fefb46e8-6901-4d50-a3f8-7c49ad72e7b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9f55c1fb1b90f676f3e1867c6aefdd13889c2cce
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188382"
---
# <a name="new-linked-report-page-report-manager"></a>새 링크된 보고서 페이지(보고서 관리자)
  새 링크된 보고서 페이지를 사용하여 링크된 보고서를 만들 수 있습니다. 링크된 보고서는 고유한 설정 및 속성은 있지만 다른 보고서의 보고서 정의에 연결되어 있는 보고서입니다. 링크된 보고서는 특정 그룹이나 사용자에 대해 변경할 기준 보고서가 있는 경우에 유용합니다. 매개 변수로 지정하는 지역 코드에 따라 다른 데이터를 반환하는 지역 보고서를 예로 들 수 있습니다. 링크된 보고서는 일반적으로 매개 변수 있는 보고서에서 내용을 변경한 다음 각 보고서 인스턴스에 다른 매개 변수 값을 저장하면 만들어집니다. 그러나 액세스 가능한 모든 보고서에서 링크된 보고서를 만들 수 있습니다.  
  
 링크된 보고서는 자체 이름, 설명, 위치, 매개 변수 속성, 보고서 실행 속성, 보고서 기록 속성, 사용 권한 및 구독을 포함할 수 있지만 보고서 정의를 제공하는 기준 보고서의 데이터 원본 속성 및 레이아웃을 사용해야 합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-new-linked-report-page-from-the-contents-page"></a>내용 페이지에서 새 링크된 보고서 페이지를 열려면  
  
1.  보고서 관리자를 열고 링크된 보고서를 만들 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **링크된 보고서 만들기**를 클릭합니다.  
  
###### <a name="to-open-the-new-linked-report-page-from-the-general-properties-page-of-a-report"></a>보고서의 일반 속성 페이지에서 새 링크된 보고서 페이지를 열려면  
  
1.  보고서 관리자를 열고 링크된 보고서를 만들 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 보고서의 일반 속성 페이지가 열립니다.  
  
4.  항목 도구 모음에서 **링크된 보고서 만들기**를 클릭합니다.  
  
## <a name="options"></a>변수  
 **이름**  
 링크된 보고서의 이름을 지정합니다. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 그러나 이름을 지정할 때 ; ? : \@ & = +, $ / * \< > | "또는 / 이름을 지정 합니다.  
  
 **설명**  
 보고서 내용에 대한 설명을 입력합니다. 이 설명은 보고서 액세스 권한이 있는 사용자의 내용 페이지에 표시됩니다.  
  
 **위치**  
 보고서를 포함하는 폴더의 경로를 지정합니다. 기본적으로 링크된 보고서는 기준 보고서의 형제 항목으로 만들어집니다. 링크된 보고서를 다른 폴더에 넣으려면 **위치 변경** 을 클릭합니다.  
  
 **확인**  
 변경 내용을 저장하고 기준 보고서의 일반 속성 페이지로 돌아가려면 **확인** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [링크 된 보고서 만들기](reports/create-a-linked-report.md)   
 [일반 속성 페이지, 보고서&#40;보고서 관리자&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
