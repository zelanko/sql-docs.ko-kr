---
title: 인코딩으로 파일 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- files [SQL Server Management Studio]
- encoding [SQL Server Management Studio]
- files [SQL Server Management Studio], encoding
ms.assetid: 919544c9-59f0-4cc6-bb2a-f1ad671eb74b
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e7a252e4e766b85c83c97ee55a5204932932ee3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180775"
---
# <a name="manage-files-with-encoding"></a>인코딩으로 파일 관리
  특정 언어와 특정 플랫폼에서 코드를 더 쉽게 표시할 수 있도록 특정 문자 인코딩을 파일과 연결할 수 있습니다.  
  
## <a name="opening-files"></a>파일 열기  
 파일을 편집하는 데 사용할 편집기를 선택할 수 있습니다.  
  
#### <a name="to-open-a-file-with-a-specific-editor"></a>특정 편집기로 파일을 열려면  
  
1.  **파일** 메뉴에서 **열기**를 가리킨 다음 **파일**을 클릭합니다.  
  
2.  **파일 열기** 대화 상자에서 파일 이름을 선택합니다.  
  
3.  **열기** 단추 옆의 화살표를 클릭한 다음 표시되는 메뉴에서**연결 프로그램** 을 클릭합니다.  
  
4.  **열려는 프로그램을 선택하십시오.** 목록에서 편집기를 선택한 다음 **열기**를 클릭합니다. 특정 인코딩과 함께 파일을 열려면 SQL 쿼리 편집기(인코딩 사용), XML 편집기(인코딩 사용) 등과 같은 인코딩 지원이 포함된 편집기를 선택합니다.  
  
## <a name="saving-files"></a>파일 저장  
 또한 유니코드 인코딩 또는 다른 코드 페이지와 함께 코드를 저장하여 서유럽어 또는 동유럽어와 같은 다양한 언어를 지원할 수 있습니다. 특정 문자 인코딩을 파일과 연결하여 해당 언어로 코드를 쉽게 표시할 수 있을 뿐만 아니라 줄 끝 형식과 연결하여 특정 운영 체제를 지원할 수 있습니다. 또한 일부 문자는 유니코드 인코딩으로 저장하지 않으면 파일 이름에 사용된 경우 이 문자를 저장할 수 없습니다.  
  
#### <a name="to-save-a-file-with-a-different-encoding-or-line-ending-type"></a>다른 인코딩 또는 줄 끝 형식으로 파일을 저장하려면  
  
1.  에 **파일** 메뉴를 클릭 하 여 **저장 \<파일 이름 >으로**합니다.  
  
2.  **다른 이름으로 파일 저장** 대화 상자에서 **저장** 단추를 확장한 다음 **인코딩하여 저장**을 클릭합니다.  
  
3.  **저장 고급 옵션** 대화 상자의 **인코딩** 목록에서 원하는 인코딩을 선택합니다.  
  
4.  **줄 끝**목록에서 원하는 줄 끝 형식을 선택합니다.  
  
    > [!NOTE]  
    >  유니코드 인코딩으로 파일을 저장할 경우 이 파일은 이진 파일로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe에 체크 인되어야 합니다. 이는 유니코드로 저장되는 파일 간의 차이점을 병합, 비교 및 표시하는 기능이 Visual SourceSafe에서 지원되지 않기 때문입니다.  
  
 Visual SourceSafe를 사용하여 ANSI, UTF8 또는 유니코드로 파일을 저장하는 경우 각각에 대한 다음 제한 사항에 주의하십시오.  
  
-   ANSI 파일은 현재 코드 페이지에서 지원되는 문자만 허용하므로 국가별 사용이 제한됩니다.  
  
-   유니코드 파일은 이진 파일로 처리되므로 공유 체크 아웃, 차이 검사 또는 병합 기능을 사용할 수 없습니다. 국제 범용 파일에서 이 형식을 사용할 수 있습니다.  
  
-   UTF8 파일의 경우에는 체크 인, 체크 아웃, 차이 검사 및 병합 중에 UTF8 파일 편집기의 문제를 일으키는 변경 내용이 적용되기 때문에 Visual SourceSafe에서 안전하게 작동하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [솔루션 및 프로젝트를 관리 하는 파일](files-that-manage-solutions-and-projects.md)   
 [파일 확장명을 코드 편집기에 연결](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
  
  