---
title: 파일을 체크 인하려면에서 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckInDialog
helpviewer_keywords:
- checking in files
ms.assetid: 0657a387-8411-4406-bef9-d262a5bfa269
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5debb7c80e7365e67d8661709b09b16f5d25b7b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812587"
---
# <a name="check-in-files"></a>파일 체크 인
  수정한 원본 제어 파일을 다른 사용자가 사용할 수 있게 만들려면 파일을 원본 제어로 체크 인해야 합니다. 파일을 체크 인하면 체크 인한 버전이 원본 제어 공급자에 기록되며 파일의 최신 버전이 됩니다.  
  
 **체크 인** 명령을 사용하여 파일을 체크 인할 수 있습니다. 이 명령을 사용하여 솔루션이나 프로젝트를 체크 인하면 솔루션이나 프로젝트의 모든 파일도 체크 인됩니다. 그러나 개별 원본 코드 파일을 체크 인할 경우 해당 파일이 속하는 프로젝트나 솔루션이 체크 인되지는 않습니다.  
  
### <a name="to-check-in-a-file"></a>파일을 체크 인하려면  
  
1.  솔루션 탐색기에서 체크 인할 파일을 마우스 오른쪽 단추로 클릭한 다음 **체크 인**을 클릭합니다.  
  
2.  **체크 인** 대화 상자가 나타나면 적절한 옵션을 선택한 다음 **확인**을 클릭합니다.  
  
     **체크인**  
     선택한 항목을 모두 체크 인합니다.  
  
     **열**  
     표시할 열 및 열이 표시되는 순서를 식별합니다.  
  
     **설명**  
     체크 인 작업과 관련한 주석을 추가합니다.  
  
     **항목 체크 인할 때 대화 상자에서 확인 표시 안 함**  
     체크 인 작업을 수행하는 동안 대화 상자를 표시하지 않습니다.  
  
     **플랫 보기**  
     체크 인하는 파일을 해당 파일의 원본 제어 연결 아래에 기본 목록으로 표시합니다.  
  
     **이름**  
     체크 인할 항목의 이름을 표시합니다. 항목은 옆에 있는 확인란이 선택된 상태로 나타납니다. 특정 항목을 체크 인하지 않으려면 확인란의 선택을 취소합니다.  
  
     **Options**  
     단추 오른쪽의 화살표를 클릭하면 원본 제어 플러그 인의 체크 인 옵션이 표시됩니다.  
  
     **정렬**  
     열 표시의 순서를 정렬합니다.  
  
     **트리 뷰**  
     체크 인하는 항목의 폴더 및 파일 계층 구조를 표시합니다.  
  
 체크 인한 파일이 공유 체크 아웃의 일부가 아니면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 환경은 파일을 즉시 체크 인하며 공유 체크 아웃의 일부이면 해당 버전을 다른 사용자가 만든 버전과 병합하라는 메시지가 나타날 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [수정 된 파일의 목록을 보려면](../../2014/database-engine/view-a-list-of-modified-files.md)   
 [체크 인 관리](../../2014/database-engine/manage-checkins.md)  
  
  
