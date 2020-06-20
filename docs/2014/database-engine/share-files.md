---
title: 파일 공유 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- sharing files
- file sharing [SQL Server]
- version control services [SQL Server], file sharing
ms.assetid: 645f5c0a-e949-4e87-8988-85e4d6128464
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 79909fcdb09e349798edfe285475f8a898c3bf04
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929024"
---
# <a name="share-files"></a>파일 공유
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 여러 원본 제어 프로젝트에서 항목을 공유할 수 있습니다. 항목을 공유할 경우 항목에 대한 모든 변경 내용이 항목이 공유되는 모든 프로젝트에 반영됩니다.  
  
 항목 공유는 원본 제어 사용자에게 다음 장점을 제공합니다.  
  
-   공유 항목을 사용하는 각 프로젝트가 항목의 개별 복사본을 저장할 필요가 없으므로 원본 제어 클라이언트와 서버 모두에서 디스크 공간이 절약됩니다. 원본 제어 공급자는 공유 항목을 하나의 중앙 위치에 저장하며 해당 항목이 공유되는 모든 프로젝트는 해당 위치에 대한 포인터를 저장합니다.  
  
-   버전 비호환성이 방지됩니다. 항목이 공유되는 모든 프로젝트가 동일한 버전의 항목을 사용하기 때문에 각 항목의 복사본이 여러 프로젝트 내에서 독립적으로 변경될 경우에 발생하는 충돌이 방지됩니다.  
  
### <a name="to-share-an-item"></a>항목을 공유하려면  
  
1.  솔루션 탐색기에서 공유 파일을 넣으려는 폴더나 프로젝트를 선택합니다.  
  
2.  **파일** 메뉴에서 **원본 제어**를 가리킨 다음 **공유**를 클릭 합니다.  
  
3.  **공유** 대상 대화 상자에서 공유할 항목의 디렉터리 목록을 검색 하 고 해당 항목을 클릭 합니다.  
  
4.  **공유**를 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [원본 제어 기본 사항](../../2014/database-engine/source-control-basics.md)  
  
  
