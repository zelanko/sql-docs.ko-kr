---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1084075fe90a752a07a7abc1feb46679bd9cf5d9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058050"
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|260|  
|이벤트 원본|SQL Server 로컬 데이터베이스 런타임 12.0|  
|구성 요소|로컬 데이터베이스 런타임 API|  
|메시지 텍스트|로컬 데이터베이스 인스턴스 폴더의 전체 경로 길이가 MAX_PATH보다 깁니다. 인스턴스 폴더에 저장 되어야 합니다: SQL Server 로컬 DB\Instances %%LOCALAPPDATA%%\Microsoft\Microsoft\\< 인스턴스 이름\>합니다.|  
  
## <a name="explanation"></a>설명  
 인스턴스를 저장할 경로가 MAX_PATH보다 깁니다.  
  
## <a name="user-action"></a>사용자 동작  
 MAX_PATH보다 길지 않은 새 경로를 만드십시오.  
  
  
