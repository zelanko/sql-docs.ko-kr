---
title: MSSQLSERVER_15661 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7b407f652dc2ef9bcca807c359120166d5f31f89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079274"
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
    
## <a name="details"></a>설명  
  
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
  
  