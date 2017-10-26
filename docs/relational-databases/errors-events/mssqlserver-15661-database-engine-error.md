---
title: "MSSQLSERVER_15661 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 93bd2efde15065f2d7285912a72a10a7ba77d817
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|15661|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum15661|  
|메시지 텍스트|sp_estimate_data_compression_savings 저장 프로시저는 임시 테이블로 사용할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
임시 테이블이 sp_estimate_data_compression_savings 저장 프로시저의 인수로 사용되었습니다. 임시 테이블을 압축할 수는 있지만 sp_estimate_data_compression_savings를 사용하여 압축 전후 크기 변경 사항을 예상할 수는 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
sp_estimate_data_compression_savings의 인수로 사용된 임시 테이블을 제거합니다.  
  

