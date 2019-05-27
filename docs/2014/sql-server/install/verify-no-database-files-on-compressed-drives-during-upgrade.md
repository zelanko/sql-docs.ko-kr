---
title: 업그레이드 프로세스 중 데이터베이스 파일이 압축 된 드라이브에 있는지 확인 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41c183c72188cccb21838e1e574992bfb723c022
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091155"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>업그레이드 프로세스 중에 데이터베이스 파일이 압축된 드라이브에 없는지 확인합니다.
  업그레이드 관리자가 압축된 드라이브에서 데이터베이스 파일을 검색했습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 압축된 드라이브에서 데이터베이스를 만들거나 업그레이드할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 설치할 때 시스템 데이터베이스에 대해 압축되지 않은 드라이브를 선택하고 업그레이드할 데이터베이스가 압축된 드라이브에 없는지 확인합니다. 데이터베이스를 업그레이드한 후에는 NTFS 압축 파일 시스템에 읽기 전용 데이터베이스 및 읽기 전용 보조 파일 그룹을 보관할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
