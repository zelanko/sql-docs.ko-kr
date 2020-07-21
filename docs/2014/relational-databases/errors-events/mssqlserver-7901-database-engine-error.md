---
title: MSSQLSERVER_7901 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6dd4d2721967049295f3fcf5fc8b38807268879a
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551060"
---
# <a name="mssqlserver_7901"></a>MSSQLSERVER_7901
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7901|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|메시지 텍스트|복구 문이 처리되지 않았습니다. 데이터베이스가 응급 모드인 경우 이 복구 수준은 지원되지 않습니다.|  
  
## <a name="explanation"></a>설명  
 데이터베이스가 응급 모드이며 REPAIR_ALLOW_DATA_LOSS 이외의 복구 수준이 지정되었습니다. REPAIR_ALLOW_DATA_LOSS를 지정하지 않는 한 응급 모드에서는 복구할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 명령을 다시 실행하고 REPAIR_ALLOW_DATA_LOSS 옵션을 지정합니다.  
  
  
