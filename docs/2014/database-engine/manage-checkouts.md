---
title: 체크 아웃 관리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], checkouts
- checkouts [SQL Server Management Studio]
- checking out files
ms.assetid: ddd4adba-d432-4005-9cb2-bb9ee3163d8e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cdfa25cdc27e707d4be705e66b215130c9d70ce1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930907"
---
# <a name="manage-checkouts"></a>체크 아웃 관리
  파일이 원본 제어에 추가된 후에 파일을 수정할 수 있으려면 먼저 체크 아웃해야 합니다. 파일을 원본 제어에서 체크 아웃할 경우 원본 제어 공급자는 로컬 디스크에서 최신 버전의 복사본을 만들고 파일의 읽기 전용 특성을 제거합니다. 경우에 따라서는 파일을 체크 아웃하지 않고 편집해야 할 수 있습니다. 파일을 체크 아웃 하지 않고 파일을 편집 하는 방법에 대 한 자세한 내용은 [체크 인 파일 편집](../../2014/database-engine/edit-checked-in-files.md)을 참조 하세요.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 사용 하 여 파일을 수동으로 또는 자동으로 체크 아웃할 수 있습니다. 환경에 파일이 포함 된 솔루션을 열고 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] **체크 아웃** 명령을 클릭 하 여 파일을 수동으로 체크 아웃 합니다. 자동으로 체크 아웃하도록 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 환경을 구성한 경우 파일을 자동으로 체크 아웃할 수 있습니다.  
  
 원본 제어 공급자에서 관리자가 설정한 옵션에 따라 파일을 배타적으로 또는 공유 모드로 체크 아웃할 수도 있습니다. 파일이 배타적으로 체크 아웃되면 파일을 체크 아웃한 사용자만 수정할 수 있으며 다른 사용자는 파일을 체크 아웃한 사용자가 체크 인할 때까지 파일을 체크 아웃할 수 없습니다. 파일이 공유 모드로 체크 아웃되면 다른 모든 사용자가 동일한 파일을 체크 아웃할 수 있습니다. 각 사용자가 파일을 체크 인할 경우 원본 제어 공급자는 파일을 파일의 최신 서버 버전으로 병합하려고 합니다. 체크 인하는 버전과 최신 버전 간에 충돌이 발생하면 원본 제어 공급자는 충돌을 해결하라는 메시지를 표시합니다.  
  
 다음 표에서는 이 섹션에서 다루는 항목에 대해 설명합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[파일 체크 아웃](../../2014/database-engine/check-out-files.md)|파일을 수정할 수 있도록 체크 아웃하는 방법에 대한 지침을 제공합니다.|  
|[체크 아웃 취소](../../2014/database-engine/undo-checkouts.md)|기존 체크 아웃을 취소하는 방법에 대해 설명합니다.|  
|[편집 시 자동으로 파일 체크 아웃](../../2014/database-engine/automatically-check-out-files-upon-edit.md)|파일 편집을 시작할 때 파일을 체크 아웃하도록 원본 제어를 구성하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [체크 인 관리](../../2014/database-engine/manage-checkins.md)   
 [체크 인 파일 편집](../../2014/database-engine/edit-checked-in-files.md)  
  
  
