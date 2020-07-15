---
title: default trace enabled 서버 구성 옵션 | Microsoft Docs
description: "\"기본 추적 설정\" 옵션에 대해 알아봅니다. 기본 추적이 어떻게 문제 해결에 도움이 될 수 있는지 확인합니다."
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], traces
- traces [SQL Server], logs
- default trace enabled option
ms.assetid: 1322d668-44f4-469e-8fd6-e0d02a81c8f2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bfeec7df441b841cbbaa5da7c0b693f37749e861
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772558"
---
# <a name="default-trace-enabled-server-configuration-option"></a>default trace enabled 서버 구성 옵션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **default trace enabled** 옵션을 사용하여 기본 추적 로그 파일을 설정하거나 해제할 수 있습니다. 기본 추적 기능은 주로 구성 옵션과 관련된 변경 내용과 작업에 대한 다양하고 영구적인 로그를 제공합니다.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
  
## <a name="purpose"></a>목적  
 기본 추적 기능은 데이터베이스 관리자가 처음 문제 발생 시 문제 진단에 필요한 로그 데이터를 가지고 있는지 확인하여 문제를 해결하도록 도와 줍니다.  
  
## <a name="viewing"></a>보기  
 기본 추적 로그는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서 열어서 검사하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 함수를 사용하여 `fn_trace_gettable` 로 쿼리할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서는 일반 추적 출력 파일을 여는 것과 똑같이 기본 추적 로그 파일을 열 수 있습니다. 기본 추적 로그는 기본적으로 롤오버 추적 파일을 사용하여 `\MSSQL\LOG` 디렉터리에 저장됩니다. 기본 추적 로그 파일의 기본 파일 이름은 `log.trc`입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]일반 설치에서는 기본 추적이 설정되므로 TraceID는 1이 됩니다. 설치 후와 다른 추적 생성 후에 기본 추적이 설정되면 TraceID가 더 큰 숫자가 될 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로파일러를 사용하여 이 추적 파일을 보는 방법은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)를 참조하세요.  
  
### <a name="example"></a>예제:  
 다음 문은 기본 위치에 있는 기본 추적 로그를 엽니다.  
  
```  
SELECT *   
FROM fn_trace_gettable  
('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\LOG\log.trc', default);  
GO  
  
```  
  
## <a name="configuring"></a>구성  
 **default trace enabled** 옵션을 1로 설정하면 **기본 추적**을 사용할 수 있습니다. 이 옵션의 기본 설정은 1(설정)입니다. 값이 0이면 추적 기능은 해제됩니다.  
  
 **default trace enabled** 옵션은 고급 옵션입니다. **sp_configure** 시스템 저장 프로시저를 사용하여 설정을 변경하는 경우 **고급 옵션 표시** 를 1로 설정한 경우에만 **기본 추적 설정** 옵션을 변경할 수 있습니다. 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
