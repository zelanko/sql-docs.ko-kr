---
title: MSSQLSERVER_948 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "948"
helpviewer_keywords:
- 948 (Database Engine error)
ms.assetid: 95c4ad45-a518-4165-a5c4-6e6b932b0570
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 74dd7dda8c743a9914f800b9cf7844de63b3dae2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85636308"
---
# <a name="mssqlserver_948"></a>MSSQLSERVER_948
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
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
원본 서버에서 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전을 확인하십시오. 이 작업은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭하거나 쿼리 창에 **SELECT @@VERSION** 을 입력하여 수행할 수 있습니다. 그런 다음 원래 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터베이스를 열어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 원래 데이터베이스에 설정되어 있는 기능을 조사한 후 데이터베이스가 연결될 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 작동하도록 이러한 설정을 수정하십시오.  
  
