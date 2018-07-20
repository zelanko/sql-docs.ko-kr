---
title: 일반 속성 페이지, 폴더 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 31d99d9b-2303-4bae-9466-fb67b97cf11a
caps.latest.revision: 25
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9418474fed667dade02caaa7eb809ee8d2e16042
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083905"
---
# <a name="general-properties-page-folders-report-manager"></a>일반 속성 페이지, 폴더(보고서 관리자)
  폴더의 일반 속성 페이지를 사용하여 만든 폴더의 속성을 보거나 설정할 수 있습니다. 폴더를 만들거나 수정한 사람 및 폴더를 수정한 시간에 대한 정보가 일반 속성 페이지 맨 위에 표시됩니다.  
  
 폴더 속성에는 보안 설정도 포함됩니다. 폴더 보안에 대 한 자세한 내용은 참조 하세요. [폴더 보안](security/secure-folders.md)합니다.  
  
 특수한 용도의 폴더(예: 홈, 내 보고서 및 사용자 폴더)는 보고서 서버 네임스페이스 내에서 이름을 바꾸거나 이동할 수 없습니다. 이 폴더에 대해서는 일반 속성 페이지를 사용할 수 없습니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-general-properties-page-for-a-folder"></a>폴더의 일반 속성 페이지를 열려면  
  
1.  보고서 관리자를 열고 속성을 보거나 구성하려는 폴더를 엽니다.  
  
2.  폴더 배너 아래의 도구 모음에서 **폴더 설정**을 클릭합니다.  
  
## <a name="options"></a>Options  
 **이름**  
 폴더의 이름을 지정합니다. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 이름을 지정할 때 ; ? : \@ & = +, $ * \< > | "또는 / 이름을 지정 합니다.  
  
 **설명**  
 폴더 내용에 대한 설명을 입력합니다. 이 설명은 해당 폴더 액세스 권한이 있는 사용자의 내용 페이지에 표시됩니다.  
  
 **목록 뷰에서 숨기기**  
 보고서 관리자에서 목록 뷰 모드를 사용하는 사용자가 볼 수 없게 폴더를 숨기려면 이 옵션을 선택합니다. 목록 뷰 모드는 보고서 서버 폴더 계층을 검색할 때 표시되는 기본 뷰 형식입니다. 목록 뷰에서 항목 이름과 설명은 페이지에 가로로 표시됩니다. 이 외에도 자세히 보기를 사용할 수 있습니다. 자세히 보기는 설명을 표시하지 않지만 항목에 대한 다른 정보는 포함합니다. 목록 뷰에서는 항목을 숨길 수 있지만 자세히 보기에서는 항목을 숨길 수 없습니다. 항목에 대한 액세스를 제한하려면 역할 할당을 만들어야 합니다.  
  
 **적용**  
 클릭하여 변경 내용을 저장합니다.  
  
 **Delete**  
 폴더 및 포함된 내용을 제거하려면 &lt;B&gt;삭제&lt;/B&gt;를 클릭합니다.  
  
 **이동**  
 보고서 서버 네임스페이스 내에서 보고서나 폴더의 위치를 다시 지정하려면 클릭합니다. 이 단추를 클릭하면 폴더를 검색하여 새 폴더 위치를 찾을 수 있는 항목 이동 페이지가 열립니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
