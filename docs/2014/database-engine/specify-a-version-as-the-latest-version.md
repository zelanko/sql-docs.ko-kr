---
title: 최신 버전으로 버전 지정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], latest version
- latest file version specified
- file versions [SQL Server]
ms.assetid: 407dffb1-3ecf-461e-835d-124781f26ee7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f34631e979ded7a329939c23a758ccc0c9aea959
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773479"
---
# <a name="specify-a-version-as-the-latest-version"></a>최신 버전으로 버전 지정
  파일을 원본 제어에 체크 인하면 체크 인한 버전은 최신 버전이 됩니다. 최신 버전을 체크 아웃하거나 검색하는 사용자는 가장 최근에 체크 인된 항목의 로컬 복사본을 받게 됩니다.  
  
 그러나 경우에 따라서는 이전 버전의 항목을 최신 버전으로 지정하려고 할 수 있습니다. 예를 들어 파일을 체크 아웃하고 수정한 다음 체크 인했는데 나중에 수정한 내용을 삭제하도록 결정할 수 있습니다. 항목을 체크 인했기 때문에 원래 체크 아웃을 실행 취소하는 것은 가능하지 않습니다. 이 경우에는 원래 체크 아웃했던 버전을 항목의 최신 버전으로 지정할 수 있습니다.  
  
 다음과 같은 방법으로 최신 버전을 지정할 수 있습니다.  
  
-   **버전 고정**합니다. 파일 버전을 고정하면 고정된 버전보다 최신인 버전은 삭제되지 않습니다. 또한 이전에 고정했던 파일을 고정 해지할 수 있습니다. 이렇게 하면 최근에 체크 인한 파일 버전이 최신 버전이 됩니다. 그러나 고정된 파일을 체크 아웃할 수는 없습니다.  
  
-   **지정된 된 버전으로 롤백**합니다. 특정 버전으로 롤백하면 롤백한 버전보다 최신인 모든 버전이 소스 제어에서 삭제됩니다. 그런 다음 나머지 최신 버전을 체크 아웃할 수 있습니다.  
  
### <a name="to-pin-a-version"></a>버전을 고정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 솔루션을 엽니다.  
  
2.  솔루션 탐색기에서 최신 버전으로 지정할 파일을 선택합니다.  
  
3.  에 **파일** 메뉴에서 **소스 제어** 누릅니다 **ViewHistory**합니다.  
  
4.  에 **기록을** \<파일 > 대화 상자에서 최신으로 지정 하 고 클릭 하려는 버전을 선택 **Pin**합니다.  
  
     최신 파일 버전이라는 것을 나타내는 고정 기호가 선택한 버전 옆에 나타납니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 로드된 다른 버전이 있을 경우 파일을 다시 로드하라는 메시지가 나타납니다.  
  
### <a name="to-roll-back-to-a-version"></a>특정 버전으로 롤백하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 솔루션을 엽니다.  
  
2.  솔루션 탐색기에서 최신 버전으로 지정할 항목을 선택합니다.  
  
3.  에 **파일** 메뉴에서 **소스 제어** 누릅니다 **기록**합니다.  
  
4.  에 **기록 옵션** 대화 상자에서 클릭 **확인** 표시할 합니다 **파일의 기록** 대화 상자.  
  
5.  에 **파일의 기록을** 상자에서 최신 버전을 지정 하 고 클릭 하려는 버전을 선택 **롤백**합니다.  
  
     선택한 버전 이후의 모든 버전이 삭제된다는 것을 알리는 메시지가 나타납니다.  
  
6.  클릭 **예** 선택한 버전으로 롤백할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [체크 인 관리](../../2014/database-engine/manage-checkins.md)   
 [파일 체크 인](../../2014/database-engine/check-in-files.md)  
  
  
