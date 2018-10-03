---
title: 체크 아웃 취소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourcControl.UndoCheckDialog
helpviewer_keywords:
- checking out files
- checkout source controls [SQL Server]
- undoing checkouts
ms.assetid: a6596b20-3aa5-4dc4-a4c5-3649f1f5a20e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2057c78f953645c9b1a5915b9912ab99263cb005
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078323"
---
# <a name="undo-checkouts"></a>체크 아웃 취소
  **체크 아웃 취소** 명령을 사용하여 기존 체크 아웃을 취소할 수 있습니다. 파일을 수정 및 저장한 다음 나중에 변경 내용을 롤백해야 하는 경우에 이 명령이 특히 유용합니다.  
  
 **체크 아웃 취소 고급 옵션** 대화 상자에서 설정한 옵션에 따라서 Studio 환경은 항목의 작업 복사본을 로컬 디스크에 그대로 두거나 해당 복사본을 최신 원본 제어 버전으로 대체합니다. 임의의 사용자가 원본 제어 시스템의 컨텍스트 외부에서 항목을 수정한 경우 검색된 버전은 최신 버전이 아닐 수 있습니다.  
  
### <a name="to-undo-a-checkout"></a>체크 아웃을 취소하려면  
  
1.  솔루션 탐색기에서 프로젝트를 선택합니다.  
  
2.  **파일** 메뉴에서 **원본 제어**를 가리킨 다음 **체크 아웃 취소**를 클릭합니다.  
  
3.  **체크 아웃 취소** 대화 상자에서 적절한 옵션을 선택한 다음 **체크 아웃 취소** 단추를 클릭합니다.  
  
     **열**  
     표시할 열 및 열이 표시되는 순서를 식별합니다.  
  
     **플랫 보기**  
     항목을 해당 원본 제어 연결 아래에 기본 목록으로 표시합니다.  
  
     **이름**  
     체크 아웃을 취소할 항목의 이름을 표시합니다. 항목은 옆에 있는 확인란이 선택된 상태로 나타납니다. 항목의 체크 아웃을 취소하지 않으려면 해당 확인란의 선택을 취소합니다.  
  
     **옵션**  
     단추 오른쪽의 화살표를 클릭하면 원본 제어 플러그 인의 체크 아웃 취소 옵션이 표시됩니다.  
  
     **Sort**  
     열 표시의 순서를 정렬합니다.  
  
     **트리 뷰**  
     체크 아웃을 되돌리고 있는 항목의 폴더 및 항목 계층 구조를 표시합니다.  
  
     **체크 아웃 취소**  
     체크 아웃된 파일의 모든 변경 내용을 삭제하고 체크 아웃을 되돌립니다.  
  
## <a name="see-also"></a>관련 항목  
 [파일을 체크 아웃](../../2014/database-engine/check-out-files.md)   
 [체크 아웃 관리](../../2014/database-engine/manage-checkouts.md)  
  
  
