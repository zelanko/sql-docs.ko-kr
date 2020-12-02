---
description: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: a4313aa27b2bae30f6eb989e2161b80635a2b985
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506227"
---
# <a name="localdb_error_instance_folder_path_too_long"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>세부 정보  
  
| attribute | 값 |
| --------- | ----- | 
|제품 이름|SQL Server|  
|이벤트 ID|260|  
|이벤트 원본|SQL Server 로컬 데이터베이스 런타임 12.0|  
|구성 요소|로컬 데이터베이스 런타임 API|  
|메시지 텍스트|로컬 데이터베이스 인스턴스 폴더의 전체 경로 길이가 MAX_PATH보다 깁니다. 인스턴스는 인스턴스 이름<%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server 로컬 DB\Instances 폴더에 저장 해야 합니다. \\ \>|  
  
## <a name="explanation"></a>설명  
 인스턴스를 저장할 경로가 MAX_PATH보다 깁니다.  
  
## <a name="user-action"></a>사용자 동작  
 MAX_PATH보다 길지 않은 새 경로를 만드십시오.  
  
  
