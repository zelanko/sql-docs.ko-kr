---
title: MSSQLSERVER_15661 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0271487ec01b29afe5485f754628d20fa4f74322
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823638"
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
