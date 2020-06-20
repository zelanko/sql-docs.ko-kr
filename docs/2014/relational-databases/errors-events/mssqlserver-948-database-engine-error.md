---
title: MSSQLSERVER_948 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "948"
helpviewer_keywords:
- 948 (Database Engine error)
ms.assetid: 95c4ad45-a518-4165-a5c4-6e6b932b0570
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e8461069a3fceb7bdca318b82a522f7f51af83d2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031382"
---
# <a name="mssqlserver_948"></a>MSSQLSERVER_948
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|948|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|해당 없음|  
|메시지 텍스트|데이터베이스 '%.*ls'은(는) 해당 버전이 %d이므로 열 수 없습니다. 이 서버는 버전 %d 및 이전 버전을 지원합니다. 다운그레이드는 지원되지 않습니다.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 기능은 데이터베이스 파일의 구조에 영향을 줍니다. 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터베이스를 연결하는 경우 파일 형식이 다른 버전의 [!INCLUDE[ssDE](../../includes/ssde-md.md)]과 호환되지 않을 수 있습니다.  
  
 예를 들어 이 오류는 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 vardecimal 스토리지 형식을 사용한 다음 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서비스 팩 2 이전 버전에서 데이터베이스 파일을 연결하려고 하여 발생할 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 원본 서버에서 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전을 확인하십시오. 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 서버를 마우스 오른쪽 단추로 클릭 한 다음 **속성** 을 클릭 하거나 `SELECT @@VERSION` 쿼리 창에서을 입력 합니다. 그런 다음 원래 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터베이스를 열어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 원래 데이터베이스에 설정되어 있는 기능을 조사한 후 데이터베이스가 연결될 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 작동하도록 이러한 설정을 수정하십시오.  
  
  
