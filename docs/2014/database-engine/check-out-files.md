---
title: 파일 체크 아웃 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- Visual Studio.SourceControl.CheckOutDialog
helpviewer_keywords:
- checking out files
ms.assetid: cc033727-51bb-4b58-a12b-8977ce61ff56
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 10c076f7bee35e0e466fc22aec9ad9f6984bac6a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936034"
---
# <a name="check-out-files"></a>파일 체크 아웃
  체크 인한 파일을 편집하는 것을 허용하도록 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 환경을 구성하지 않은 경우 파일을 수정할 수 있으려면 체크 아웃해야 합니다. 파일을 체크 아웃하면 파일 버전의 복사본이 로컬 디스크에 복사되며 파일의 읽기 전용 특성이 제거됩니다.  
  
 파일을 배타적으로 또는 공유 모드로 체크 아웃할 수 있습니다. 파일이 배타적으로 체크 아웃되면 체크 아웃한 사용자가 체크 인할 때까지 다른 사용자가 파일을 체크 아웃할 수 없습니다. 파일이 공유 모드로 체크 아웃되면 다른 사용자가 파일을 체크 아웃 및 수정할 수 있으며 파일을 체크 인할 경우에는 자신이 체크 아웃한 버전과 다른 사용자가 만든 버전을 병합해야 할 수 있습니다.  
  
 **체크 아웃** 명령을 사용하여 원본 제어 프로젝트와 파일을 체크 아웃할 수 있습니다. 이 명령을 사용 하 여 솔루션이 나 프로젝트를 체크 아웃 하면 솔루션이 나 프로젝트의 모든 파일도 체크 아웃 됩니다. 그러나 개별 원본 코드 파일을 체크 아웃 하면 해당 파일에 속한 프로젝트 또는 솔루션이 체크 아웃 되지 않습니다.  
  
> [!NOTE]  
>  프로젝트에 대한 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 데이터베이스가 여러 체크 아웃을 허용하도록 구성된 상태에서 파일을 배타적으로 체크 아웃하려는 경우에는 파일을 체크 아웃하기 전에 **고급 체크 아웃 옵션** 대화 상자에서 **여러 체크 아웃 허용** 옵션을 선택 취소해야 합니다. 이 설정을 적용하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 다시 시작해야 합니다.  
  
### <a name="to-check-out-a-file"></a>파일을 체크 아웃하려면  
  
1.  솔루션 탐색기에서 프로젝트나 파일을 선택합니다.  
  
2.  **파일** 메뉴에서 **원본 제어**를 가리킨 다음 **편집하기 위해 체크 아웃**을 클릭합니다.  
  
3.  **편집 하기 위해 체크 아웃** 대화 상자가 표시 되 면 원하는 항목을 선택 하 고 **체크 아웃**을 클릭 합니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] **체크 아웃** 대화 상자를 표시 하지 않도록 환경을 구성한 경우 솔루션 탐색기에서 선택한 항목과 해당 항목이 있을 수 있는 모든 자식 항목이 즉시 체크 아웃 됩니다.  
  
     **체크 아웃**  
     선택한 항목을 모두 체크 아웃합니다.  
  
     **열**  
     표시할 열 및 열이 표시되는 순서를 식별합니다.  
  
     **설명**  
     체크 아웃 작업과 관련한 설명을 지정합니다.  
  
     **체크 아웃할 때 체크 아웃 대화 상자 표시 안 함**  
     체크 아웃 작업을 실행하는 동안 대화 상자를 표시하지 않습니다.  
  
     **기본 뷰**  
     체크 아웃하는 항목을 해당 원본 제어 연결 아래에 기본 목록으로 표시합니다.  
  
     **편집**  
     항목을 체크 아웃 하지 않고 수정 합니다. **편집** 단추는 체크 인 된 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 파일의 편집을 지원 하도록를 구성한 경우에만 표시 됩니다.  
  
     **이름**  
     체크 아웃할 수 있는 항목의 이름을 표시합니다. 항목은 옆에 있는 확인란이 선택된 상태로 나타납니다. 특정 항목을 체크 아웃하지 않으려면 확인란의 선택을 취소합니다.  
  
     **Options**  
     단추 오른쪽의 화살표를 클릭하면 원본 제어 플러그 인의 체크 아웃 옵션이 표시됩니다.  
  
     **정렬**  
     표시된 열의 순서를 정렬합니다.  
  
     **트리 뷰**  
     체크 아웃하는 항목의 폴더 및 파일 계층 구조를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [체크 인 한 파일 편집](../../2014/database-engine/edit-checked-in-files.md)   
 [편집 시 자동으로 파일 체크 아웃](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [체크 아웃 취소](../../2014/database-engine/undo-checkouts.md)   
 [체크 아웃 관리](../../2014/database-engine/manage-checkouts.md)  
  
  
