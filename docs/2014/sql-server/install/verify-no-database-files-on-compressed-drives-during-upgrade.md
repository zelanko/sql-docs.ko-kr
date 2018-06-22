---
title: 업그레이드 프로세스 중 데이터베이스 파일이 압축 된 드라이브에서이 확인 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 59370b953c377e983f58c3037a7920de0076bd56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079195"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>업그레이드 프로세스 중에 데이터베이스 파일이 압축된 드라이브에 없는지 확인합니다.
  업그레이드 관리자가 압축된 드라이브에서 데이터베이스 파일을 검색했습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 압축된 드라이브에서 데이터베이스를 만들거나 업그레이드할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 설치할 때 시스템 데이터베이스에 대해 압축되지 않은 드라이브를 선택하고 업그레이드할 데이터베이스가 압축된 드라이브에 없는지 확인합니다. 데이터베이스를 업그레이드한 후에는 NTFS 압축 파일 시스템에 읽기 전용 데이터베이스 및 읽기 전용 보조 파일 그룹을 보관할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;new&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
