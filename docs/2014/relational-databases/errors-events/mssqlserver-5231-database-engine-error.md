---
title: MSSQLSERVER_5231 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa4307f1cd72ea797ccf0a607796dca32ef4e1e6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411612"
---
# <a name="mssqlserver5231"></a>MSSQLSERVER_5231
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|5231|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|메시지 텍스트|개체 ID O_ID(개체 'NAME'): 확인을 위해 이 개체를 잠그는 동안 교착 상태가 발생했습니다. 이 개체를 건너뛰었으므로 처리되지 않습니다.|  
  
## <a name="explanation"></a>설명  
 DBCC가 개체를 잠그려고 할 때 교착 상태가 발생하여 DBCC 실행이 중지되었습니다. 개체가 처리되지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
 InclusionThresholdSetting  
  
  
