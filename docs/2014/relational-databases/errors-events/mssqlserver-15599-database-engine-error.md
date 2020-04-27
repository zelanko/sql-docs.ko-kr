---
title: MSSQLSERVER_15599 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e1e4988bea932b8279a1d5b754ef3d0271e3aa1c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915523"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|15599|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|메시지 텍스트|로컬 임시 개체에 대한 감사와 권한을 설정할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 로컬 또는 전역 임시 개체에 대해 감사와 권한을 설정해도 적용되지 않습니다. 문을 실행할 경우 오류가 발생하지는 않지만(작업에서 성공 결과가 반환됨) 적용되지 않습니다.  
  
 이 동작은 변경되지 않았지만 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 사용자에게 이 정보 메시지가 표시됩니다.  
  
## <a name="user-action"></a>사용자 동작  
 별도의 동작이 필요 없지만, 로컬 또는 전역 임시 개체에 대해 감사 또는 권한을 설정하는 문을 제거해 보십시오.  
  
  
