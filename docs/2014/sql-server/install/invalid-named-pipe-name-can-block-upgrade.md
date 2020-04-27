---
title: 잘못 된 명명 된 파이프 이름으로 업그레이드를 차단할 수 있습니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dddd5da66f09226579a6366baa1a16a6ab00d6bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094188"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>명명된 파이프 이름이 잘못된 이름이면 업그레이드가 중단될 수 있습니다.
  명명된 파이프 프로토콜이 잘못 구성된 경우 업그레이드할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 하는 동안 설치 프로그램은 로컬 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 연결만 허용 하는 명명 된 파이프와 공유 메모리 지원을 통해 인스턴스를 시작 합니다. 서버에 지정 된 파이프 이름이 비어 있지 않으면 문자열 "\\\\.\pipe\\"로 시작 하 여 유효 해야 합니다. 파이프 이름이 유효하지 않은 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 시작되지 않고 설치가 실패합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 네트워크 유틸리티를 사용 하 여 유효한 파이프 이름을 제공한 다음 설치 프로그램을 실행 합니다. ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
