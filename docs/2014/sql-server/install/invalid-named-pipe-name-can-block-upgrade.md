---
title: 잘못 된 명명 된 파이프 이름이 면 업그레이드가 중단 수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c94c1eeff18bff698e2a6353e29b72dd33278d03
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088998"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>명명된 파이프 이름이 잘못된 이름이면 업그레이드가 중단될 수 있습니다.
  명명된 파이프 프로토콜이 잘못 구성된 경우 업그레이드할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 하는 동안 설치 프로그램이 시작 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 공유 메모리 지원을 통해 인스턴스은 로컬 연결만 허용 하는 명명된 된 파이프 합니다. 문자열으로 시작 해야 서버에서 지정 된 파이프 이름이 비어 있지 않은 경우 "\\\\. \pipe\\" 유효 합니다. 파이프 이름이 유효하지 않은 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 시작되지 않고 설치가 실패합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 사용 하 여는  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 유틸리티** 을 유효한 파이프 이름을 제공한 다음 설치 프로그램을 실행 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
