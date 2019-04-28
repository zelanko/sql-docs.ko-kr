---
title: MSSQLSERVER_3169 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 57a63d884dabb1ad2e0e5d8b13dea4190dfa65de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868917"
---
# <a name="mssqlserver3169"></a>MSSQLSERVER_3169
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3169|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|NA|  
|메시지 텍스트|버전 %ls이(가) 실행되는 서버에서 데이터베이스가 백업되었습니다. 해당 버전은 버전 %ls이(가) 실행되는 이 서버와 호환되지 않습니다. 백업을 지원하는 서버에서 데이터베이스를 복원하거나 이 서버와 호환되는 백업을 사용하십시오.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 기능은 데이터베이스 파일의 구조에 영향을 줍니다. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터베이스를 복원하는 경우 파일 형식이 다른 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 호환되지 않을 수 있습니다.  
  
 예를 들어 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 vardecimal 저장소 형식을 사용한 다음 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2 이전 버전에서 데이터베이스 파일을 복원하려고 하면 이 오류가 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 원본 서버에서 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전을 확인하십시오. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 하거나 서버를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성** 종류나 `SELECT @@VERSION` 쿼리 창에서. 그런 다음 원래 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터베이스를 열어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 원래 데이터베이스에 설정되어 있는 기능을 조사한 후 데이터베이스가 복원될 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 작동하도록 이러한 설정을 수정하십시오.  
  
  
