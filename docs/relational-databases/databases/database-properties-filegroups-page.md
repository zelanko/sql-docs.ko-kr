---
title: "데이터베이스 속성(파일 그룹 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.filegroups.f1
ms.assetid: 8d06e859-73dd-4019-b6e8-99c5c5297697
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f255edfb8c5a07df31622cc19c1484d36ccd24a6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="database-properties-filegroups-page"></a>데이터베이스 속성(파일 그룹 페이지)
  이 페이지를 사용하여 파일 그룹을 확인하거나 선택한 데이터베이스에 새 파일 그룹을 추가할 수 있습니다. 파일 그룹 유형은 *행* 파일 그룹, FILESTREAM 데이터 및 메모리 최적화 파일 그룹으로 구분됩니다.  
  
 행 파일 그룹에는 일반 데이터 파일 및 로그 파일이 있고, FILESTREAM 데이터 파일 그룹에는 FILESTREAM 데이터 파일이 있습니다. 이러한 데이터 파일은 FILESTREAM 저장소를 사용할 경우 BLOB(Binary Large Object) 데이터가 파일 시스템에 저장되는 방식에 대한 정보를 저장합니다. 옵션은 두 가지 파일 그룹 유형에서 동일합니다.  
  
 FILESTREAM이 설정되지 않은 경우 **Filestream** 섹션은 사용할 수 없습니다. [서버 속성(고급 페이지)](../../database-engine/configure-windows/server-properties-advanced-page.md)을 사용하여 FILESTREAM 저장소를 설정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 파일 그룹을 사용하는 방법은 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하세요. FILESTREAM 데이터 및 파일 그룹에 대한 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
 데이터베이스가 메모리 최적화 테이블을 하나 이상 포함하려면 메모리 최적화 파일 그룹이 필요합니다.  
  
## <a name="row-and-filestream-data-filegroup-options"></a>행 및 FILESTREAM 데이터 파일 그룹 옵션  
 **이름**  
 파일 그룹의 이름을 입력합니다.  
  
 **파일**  
 파일 그룹의 파일 수를 표시합니다.  
  
 **읽기 전용**  
 파일 그룹을 읽기 전용 상태로 설정하려면 선택합니다.  
  
 **기본값**  
 이 파일 그룹을 기본 파일 그룹으로 만들려면 선택합니다. 행 및 FILESTREAM 데이터에 대해 각각 한 개의 기본 파일 그룹을 가질 수 있습니다.  
  
 **추가**  
 데이터베이스에 대한 파일 그룹을 나열하는 표에 빈 행을 새로 추가합니다.  
  
 **제거**  
 표에서 선택한 파일 그룹 행을 제거합니다.  
  
## <a name="memory-optimized-data-filegroup-options"></a>메모리 액세스에 최적화된 데이터 파일 그룹 옵션  
 **이름**  
 메모리 최적화 파일 그룹의 이름을 입력합니다.  
  
 **Filestream 파일**  
 메모리 최적화 데이터 파일 그룹에 있는 파일(컨테이너)의 수를 표시합니다. **파일** 페이지에서 컨테이너를 추가할 수 있습니다.  
  
 **추가**  
 데이터베이스에 대한 파일 그룹을 나열하는 표에 빈 행을 새로 추가합니다.  
  
 **제거**  
 표에서 선택한 파일 그룹 행을 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
