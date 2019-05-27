---
title: 업그레이드 프로세스 중에 모든 파일 그룹이 쓰기 가능한 지 확인 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- filegroups [SQL Server], writeable
- writeable filegroups [SQL Server]
ms.assetid: 2985efc1-4b14-46c3-abbd-a656b159f23c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 758207977c8ddf92d6696dda71a8943e6a596d4d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091193"
---
# <a name="verify-all-filegroups-are-writeable-during-the-upgrade-process"></a>업그레이드 프로세스 중에 모든 파일 그룹이 쓰기 가능한지 확인합니다.
  업그레이드 관리자가 하나 이상의 파일 그룹이 있는 데이터베이스를 검색했습니다. 업그레이드하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 모든 데이터베이스의 파일 그룹을 READ_WRITE로 설정해야 합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 ALTER DATABASE를 사용하여 파일을 그룹을 READ_WRITE로 설정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
