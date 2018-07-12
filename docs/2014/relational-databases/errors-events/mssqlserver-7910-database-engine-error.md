---
title: MSSQLSERVER_7910 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 7910 (Database Engine error)
ms.assetid: 017a0113-2b17-40b3-a419-30bbc43d46b8
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d3121c45b9abdf5d9985bfcbcca7f360430a7c63
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415862"
---
# <a name="mssqlserver7910"></a>MSSQLSERVER_7910
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7910|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_REPAIR_PAGE_ALLOCATED|  
|메시지 텍스트|복구: 페이지 P_ID이(가) 개체 ID O_ID, 인덱스 ID I_ID, 파티션 ID PN_ID, 할당 단위 ID A_ID(TYPE 유형)에 할당되었습니다.|  
  
## <a name="explanation"></a>설명  
 이 메시지는 페이지가 IAM(Index Allocation Map) 페이지의 단일 페이지 슬롯 배열에 할당되었음을 나타내는 REPAIR의 정보 메시지입니다.  
  
## <a name="user-action"></a>사용자 동작  
 InclusionThresholdSetting  
  
  
