---
title: 잘못 된 명명 된 파이프 이름을 업그레이드를 차단할 수 있습니다 | Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094188"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>명명된 파이프 이름이 잘못된 이름이면 업그레이드가 중단될 수 있습니다.
  명명된 파이프 프로토콜이 잘못 구성된 경우 업그레이드할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 하는 동안 설치 프로그램을 시작 합니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 공유 메모리 지원을 통해 인스턴스, 로컬 연결만 허용 하는 명명된 된 파이프 합니다. 문자열을 사용 하 여 시작 해야 서버에서 지정한 파이프 이름이 비어 있으면 "\\\\. \pipe\\" 유효 합니다. 파이프 이름이 유효하지 않은 경우에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 시작되지 않고 설치가 실패합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 사용 된  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 유틸리티** 유효한 파이프 이름을 제공한 다음 설치 프로그램을 실행 하 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
