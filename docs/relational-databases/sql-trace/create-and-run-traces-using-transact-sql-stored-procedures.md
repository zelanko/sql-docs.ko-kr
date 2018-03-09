---
title: "TRANSACT-SQL 저장 프로시저를 사용하여 추적 만들기 및 실행 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0fd60011006d595a7ff771c65ba0d3bbe3b7de75
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>TRANSACT-SQL 저장 프로시저를 사용하여 추적 만들기 및 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] SQL 추적을 사용한 추적 프로세스는 추적을 만들고 실행하는 데 Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용할지 아니면 시스템 저장 프로시저를 사용할지에 따라 달라집니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]대신 [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저를 사용하여 추적을 만들고 실행할 수 있습니다. 시스템 저장 프로시저를 사용한 추적 프로세스는 다음과 같습니다.  
  
1.  **sp_trace_create**를 사용하여 추적을 만듭니다.  
  
2.  **sp_trace_setevent**를 사용하여 이벤트를 추가합니다.  
  
3.  (옵션) **sp_trace_setfilter**를 사용하여 필터를 설정합니다.  
  
4.  **sp_trace_setstatus**를 사용하여 추적을 시작합니다.  
  
5.  **sp_trace_setstatus**를 사용하여 추적을 중지합니다.  
  
6.  **sp_trace_setstatus**를 사용하여 추적을 닫습니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저를 사용하여 서버 쪽 추적을 만들 경우 디스크에 공간이 있고 쓰기 오류가 발생하지 않는 한 이벤트가 손실되지 않습니다. 디스크가 꽉 차거나 실패하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 계속 실행되지만 추적은 중지됩니다. **c2 audit mode** 가 설정되고 쓰기가 실패하는 경우 추적이 중지되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 종료됩니다. **c2 audit mode** 설정에 대한 자세한 내용은 [c2 audit mode 서버 구성 옵션](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL 추적 최적화](../../relational-databases/sql-trace/optimize-sql-trace.md)|추적이 시스템 성능에 미치는 영향을 줄이는 방법을 설명합니다.|  
|[추적 필터링](../../relational-databases/sql-trace/filter-a-trace.md)|추적에 필터를 사용하는 방법을 설명합니다.|  
|[추적 파일 및 테이블 크기 제한](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)|추적 데이터가 기록되는 파일 및 테이블의 크기를 제한하는 방법을 설명합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서만 테이블에 추적 정보를 쓸 수 있습니다.|  
|[예약된 추적](../../relational-databases/sql-trace/schedule-traces.md)|추적 시작 시간 및 종료 시간을 설정하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_create&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
