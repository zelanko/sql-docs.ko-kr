---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
author: stevestein
ms.author: sstein
ms.openlocfilehash: aa6db2af138bb2aeefb1a922e55db56c4ea821f9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051190"
---
# <a name="localdb_error_instance_exists_with_lower_version"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|258|  
|이벤트 원본|SQL Server 로컬 데이터베이스 런타임 12.0|  
|구성 요소|로컬 데이터베이스 런타임 API|  
|메시지 텍스트|지정된 버전의 로컬 데이터베이스 인스턴스를 만들 수 없습니다. 같은 이름의 인스턴스가 이미 존재하지만 지정된 버전보다 하위 버전입니다.|  
  
## <a name="explanation"></a>설명  
 지정한 인스턴스가 이미 있지만 버전이 요청한 것보다 낮습니다.  
  
## <a name="user-action"></a>사용자 동작  
 기존 인스턴스를 삭제하고 작업을 다시 시도하십시오.  
  
  
