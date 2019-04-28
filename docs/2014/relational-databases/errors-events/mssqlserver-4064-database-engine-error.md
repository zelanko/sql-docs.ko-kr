---
title: MSSQLSERVER_4064 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69332b6d2830c53d5a3f9956443d123fd52485b3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868030"
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|4064|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DB_UFAIL_FATAL|  
|메시지 텍스트|사용자 기본 데이터베이스를 열 수 없습니다. 로그인이 실패했습니다.|  
  
## <a name="explanation"></a>설명  
SQL Server 로그인의 기본 데이터베이스 문제로 인해 로그인 시 연결하지 못했습니다. 데이터베이스 자체가 잘못되었거나 로그인에 데이터베이스에 대한 CONNECT 권한이 부족합니다.  
  
## <a name="user-action"></a>사용자 동작  
ALTER LOGIN을 사용하여 로그인의 기본 데이터베이스를 변경합니다. 로그인에 CONNECT 권한을 부여합니다.  
  
