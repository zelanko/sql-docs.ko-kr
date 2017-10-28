---
title: "추적 파일 및 테이블 크기 제한 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- maximum file size for traces
- traces [SQL Server], file size
- size [SQL Server], tables
- file rollover option [SQL Server]
- size [SQL Server], files
ms.assetid: 88c31b02-f44c-4a14-be8b-437f2097de12
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 88ac44b6c82349c1c0294a512a24ffacd6002ad3
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="limit-trace-file-and-table-sizes"></a>추적 파일 및 테이블 크기 제한
  SQL 추적 파일의 크기는 추적에 포함된 이벤트 클래스와 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 사용되는 방식에 따라 달라집니다. 자주 발생하는 이벤트 클래스를 추적하는 경우 최대 파일 크기나 최대 행 수를 설정하여 추적을 통해 수집되는 데이터의 양을 최소화할 수 있습니다. 최대 파일 크기나 최대 행 수를 지정하면 추적 파일이나 테이블의 크기가 지정된 한도를 초과하지 않습니다.  
  
> [!NOTE]  
>  추적 데이터를 기존 파일에 저장할 때는 데이터를 파일 끝에 추가하거나 기존 파일을 덮어쓸 수 있습니다. 데이터를 파일에 추가할 때 추적 파일이 지정된 최대 크기에 도달하거나 이 크기를 넘어서면 최대 파일 크기를 늘리거나 새 파일을 지정할 수 있습니다. 추적 테이블에서도 마찬가지입니다.  
  
## <a name="maximum-file-size"></a>최대 파일 크기  
 추적 파일의 최대 크기가 지정된 경우 최대 파일 크기에 도달하면 추적 정보가 더 이상 파일로 저장되지 않습니다. 이 옵션을 사용하면 이벤트를 더 작고 관리하기 쉬운 파일로 그룹화할 수 있습니다. 또한 파일 크기를 제한하면 최대 파일 크기에 도달할 때 추적이 중지되므로 무인 추적을 안전하게 실행할 수 있습니다. Transact-SQL 저장 프로시저나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 만든 추적 파일의 최대 크기를 설정할 수 있습니다.  
  
 최대 파일 크기 옵션은 최대 1GB로 제한됩니다. 최대 파일 크기의 기본값은 5MB입니다.  
  
### <a name="enabling-file-rollover"></a>파일 롤오버 사용  
 파일 롤오버 옵션을 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 최대 파일 크기에 도달하면 현재 파일을 닫고 새 파일을 만듭니다. 새 파일은 이전 파일과 같은 이름을 갖지만 순서를 나타내는 정수가 이름에 추가됩니다. 예를 들어 원래 추적 파일 이름이 filename_1.trc이면 다음 추적 파일 이름은 filename_2.trc가 되는 식으로 지정됩니다. 새 롤오버 파일에 지정된 이름이 기존 파일 이름과 같을 경우 기존 파일이 읽기 전용이 아니면 이 파일을 덮어씁니다. 추적 데이터를 파일로 저장할 때 파일 롤오버 옵션이 기본적으로 사용됩니다.  
  
> [!NOTE]  
>  파일 롤오버 옵션이 설정되어 있으면 추적은 다른 방법으로 중단되기 전까지 계속됩니다. 파일 크기 제한에 도달한 후 추적을 중지하려면 파일 롤오버 옵션을 사용하지 마십시오.  
  
 **추적 파일에 최대 파일 크기를 설정하려면**  
  
 [추적 파일에 최대 파일 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
## <a name="maximum-number-of-rows"></a>최대 행 수  
 최대 행 수가 설정된 추적은 최대 행 수에 도달할 경우 추적 정보를 테이블로 저장하는 작업이 중지됩니다. 각 이벤트는 한 행으로 구성되므로 이 매개 변수는 수집되는 이벤트 수를 제한합니다. 최대 행 수를 설정하면 무인 추적을 쉽게 실행할 수 있습니다. 예를 들어 테이블에 추적 데이터를 저장하는 추적을 시작하고 테이블이 너무 커지면 추적을 중지하는 과정을 자동으로 수행할 수 있습니다.  
  
 최대 행 수를 지정한 경우 행 수가 이 값에 도달하면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 실행 중인 경우에는 계속 추적하지만 추적 정보는 기록되지 않습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 추적이 중지될 때까지 추적 결과를 계속 표시합니다.  
  
 **추적의 최대 행 수를 설정하려면**  
  
 [추적 테이블에 최대 테이블 크기 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_create&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)  
  
  

