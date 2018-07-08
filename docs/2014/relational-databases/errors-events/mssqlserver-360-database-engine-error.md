---
title: MSSQLSERVER_360 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 73d114cbde0e5b4e132d2a39e222ecff34b66df4
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413672"
---
# <a name="mssqlserver360"></a>MSSQLSERVER_360
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|360|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DML_UPDATE_SPARSE_AND_COLSET|  
|메시지 텍스트|INSERT, UPDATE 또는 MERGE 문의 대상 열 목록은 스파스 열과 스파스 열이 포함된 열 집합을 모두 포함할 수는 없습니다. 스파스 열 또는 열 집합 중 하나만 포함하도록 문을 다시 작성하십시오.|  
  
## <a name="explanation"></a>설명  
 열 집합은 일부 테이블 열을 구조화된 출력으로 결합하는 형식화되지 않은 XML 표현입니다. 열 집합 및 열 집합에 포함된 열을 모두 수정하려고 했습니다. 이로 인해 동일한 열에 대한 참조가 두 개 만들어집니다.  
  
## <a name="user-action"></a>사용자 동작  
 열 또는 열 집합 중 하나에 대한 참조만 포함하도록 문을 다시 작성합니다.  
  
  
