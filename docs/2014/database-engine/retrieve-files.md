---
title: 파일 검색 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], file retrieval
- file retrieval [SQL Server]
- retrieving files
ms.assetid: 37b74426-e262-43b2-a81f-79b1fd1a36ec
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 548fac7dbc7d1f2750a130da9847be406361d8bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62843669"
---
# <a name="retrieve-files"></a>파일 검색
  소스 제어 프로젝트를 연 후에 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 원본 제어 저장소에서 프로젝트가 상주하는 로컬 디렉터리로 프로젝트 파일의 로컬 복사본을 검색할 수 있습니다.  
  
 통합 소스 제어를 사용하여 다음 방법으로 파일을 검색할 수 있습니다.  
  
-   **최신 버전 가져오기 (하위 폴더)** 명령  
  
     선택한 파일 중에 체크 인한 최신 버전을 검색합니다. 솔루션이나 프로젝트가 선택되면 이 명령은 모든 솔루션과 프로젝트 파일의 최신 버전을 검색합니다.  
  
-   **Get** 명령  
  
     선택 된 파일의 최신 버전을 검색 하거나 선택한 솔루션 또는 프로젝트에서 파일의 하위 집합을 검색 하는 데 사용할 수 있는 **가져오기** 대화 상자를 표시 합니다.  
  
### <a name="to-retrieve-the-latest-version-of-all-the-files-in-a-project"></a>프로젝트에 있는 모든 파일의 최신 버전을 검색하려면  
  
1.  솔루션 탐색기에서 프로젝트를 선택합니다.  
  
2.  **파일** 메뉴에서 **원본 제어**를 가리킨 다음 **최신 버전 가져오기 (하위 폴더 포함)** 를 클릭 합니다.  
  
 프로젝트에 있는 파일의 최신 버전이 로컬 디스크의 프로젝트 위치로 검색됩니다.  
  
#### <a name="to-retrieve-only-certain-files-in-a-project"></a>프로젝트의 특정 파일만 검색하려면  
  
1.  솔루션 탐색기에서 검색할 항목을 선택합니다.  
  
2.  **파일** 메뉴에서 **원본 제어**를 가리킨 다음 **가져오기**를 클릭 합니다.  
  
3.  **가져오기** 대화 상자에서 **확인**을 클릭 합니다. 또는 솔루션 탐색기에서 솔루션이나 프로젝트를 선택한 경우 검색하지 않으려는 항목 옆에 있는 확인란의 선택을 취소합니다.  
  
## <a name="see-also"></a>참고 항목  
 [소스 제어를 &#40;대화 상자를 가져옵니다&#41;](../../2014/database-engine/get-dialog-box-source-control.md)   
 [버전 정보 설정 및 검색](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [프로젝트 기록 보기](../../2014/database-engine/view-project-history.md)   
 [파일 상태 보기](../../2014/database-engine/view-file-status.md)  
  
  
