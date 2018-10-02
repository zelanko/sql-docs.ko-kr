---
title: MSSQLSERVER_21862 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21862 (Database Engine error)
ms.assetid: a1d393dd-453b-4d45-9aa5-7d371213e32b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 331e07fce8dc82ee090f3e28c8281ed29514fd46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624713"
---
# <a name="mssqlserver21862"></a>MSSQLSERVER_21862
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
데이터베이스 스냅숏을 통해 FILESTREAM 데이터에 액세스할 수 없으므로 게시의 동기화 메서드에 대해 *database snapshot* 또는 *database_snapshot_character* 매개 변수를 지정하면 스냅숏 에이전트가 FILESTREAM 데이터를 읽을 수 없게 됩니다.  
  
## <a name="user-action"></a>사용자 동작  
게시 동기화 메서드를 *database snapshot* 또는 *database_snapshot_character*가 아닌 다른 것으로 변경하거나 게시에서 FILESTREAM 열을 제외하세요.  
  
