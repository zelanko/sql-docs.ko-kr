---
title: MSSQLSERVER_9790 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84e445191cb6b4783d46bb0ec67f71bda93e1a58
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34324854"
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9790|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|메시지 텍스트|들어오는 메시지를 라우팅할 수 없습니다. 라우팅 정보를 포함하는 시스템 데이터베이스 MSDB가 단일 사용자 모드입니다.|  
  
## <a name="explanation"></a>설명  
MSDB 데이터베이스가 단일 사용자 모드에 있었기 때문에 네트워크를 통해 수신한 메시지를 분류하려고 하는 동안 오류가 발생했습니다.  
  
## <a name="user-action"></a>사용자 동작  
ALTER DATABASE 명령을 사용하여 MSDB를 다중 사용자 모드로 변경합니다.  
  
