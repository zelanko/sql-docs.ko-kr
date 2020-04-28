---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: stevestein
ms.author: sstein
ms.openlocfilehash: 372ec1bbee84b90a9a30ec768fd7a35e3f6112d5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67995790"
---
# <a name="localdb_error_insufficient_buffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|276|  
|이벤트 원본|SQL Server 로컬 데이터베이스 런타임 12.0|  
|구성 요소|로컬 데이터베이스 런타임 API|  
|메시지 텍스트|로컬 데이터베이스 인스턴스 API 메서드로 전달된 버퍼의 크기가 부족합니다.|  
  
## <a name="explanation"></a>설명  
 입력 버퍼가 너무 짧은데 잘림이 요청되지 않았습니다.  
  
## <a name="user-action"></a>사용자 동작  
 지정된 크기의 버퍼를 제공하십시오.  
  
  
