---
title: MSSQLSERVER_21862 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f336c64ffc0d044fa0f7282f3c87451483353879
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914954"
---
# <a name="mssqlserver_21862"></a>MSSQLSERVER_21862
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|21862|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum21862|  
|메시지 텍스트|'database snapshot' 또는 'database snapshot character' 동기화 메서드를 사용하여 게시에 FILESTREAM 열을 게시할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 데이터베이스 스냅샷을 통해 FILESTREAM 데이터에 액세스할 수 없으므로 게시의 동기화 메서드에 대해 *database snapshot* 또는 *database_snapshot_character* 매개 변수를 지정하면 스냅샷 에이전트가 FILESTREAM 데이터를 읽을 수 없게 됩니다.  
  
## <a name="user-action"></a>사용자 동작  
 게시 동기화 메서드를 *database snapshot* 또는 *database_snapshot_character*가 아닌 다른 것으로 변경하거나 게시에서 FILESTREAM 열을 제외하세요.  
  
  
