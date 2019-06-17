---
title: MSSQLSERVER_9524 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16f5876211a987dff593721310ee31667d428b81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761662"
---
# <a name="mssqlserver9524"></a>MSSQLSERVER_9524
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9254|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|XMLERR_INVALID_COLUMNSET_XML|  
|메시지 텍스트|제공한 XML 내용이 스파스 열 집합의 필수 XML 형식에 맞지 않습니다.|  
  
## <a name="explanation"></a>설명  
 열 집합을 수정하려고 했습니다. 열 집합의 XML 내용은 열 집합의 형식 제한 사항을 충족해야 합니다. 일반 열 집합 형식은 다음과 같습니다.  
  
 `<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
 열 집합에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "열 집합 사용" 항목을 참조하십시오.  
  
## <a name="user-action"></a>사용자 동작  
 문에 포함된 열 집합의 XML 형식을 수정합니다.  
  
  
