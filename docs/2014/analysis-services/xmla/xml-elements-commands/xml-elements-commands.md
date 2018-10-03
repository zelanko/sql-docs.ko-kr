---
title: 명령 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5e51d1989b3c492814f5958bacd82bbc01ef76d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105383"
---
# <a name="commands-xmla"></a>명령(XMLA)
  이 참조 섹션에서는 `Command` 메서드 호출 시 `Execute` 요소에서 사용할 수 있는 XMLA(XML for Analysis) 요소를 다룹니다.  
  
|요소|Description|  
|-------------|-----------------|  
|[Alter 요소(XMLA)](alter-element-xmla.md)|사용 되는 Analysis Services Scripting Language (ASSL) 요소를 포함 합니다 [Execute](../xml-elements-methods-execute.md) 인스턴스의 개체를 변경 하는 방법 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|[Backup 요소](backup-element-xmla.md)|백업 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 백업 파일입니다.|  
|[Batch 요소](batch-element-xmla.md)|순차 또는 병렬 인스턴스의 Analysis (XMLA) 명령에 대 한 하나 이상의 XML을 일괄 처리 작업으로 수행 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|[BeginTransaction 요소](begintransaction-element-xmla.md)|Analysis Services 인스턴스로 현재 세션에서 트랜잭션을 시작합니다.|  
|[Cancel 요소](cancel-element-xmla.md)|Analysis Services 인스턴스에서 현재 실행 중인 명령을 취소합니다.|  
|[ClearCache 요소](clearcache-element-xmla.md)|Analysis Services 인스턴스에서 지정된 개체의 메모리 캐시를 지웁니다.|  
|[CommitTransaction 요소](committransaction-element-xmla.md)|Analysis Services 인스턴스로 현재 세션에서 트랜잭션을 커밋합니다.|  
|[Create 요소](create-element-xmla.md)|사용 되는 Analysis Services Scripting Language (ASSL) 요소를 포함 합니다 [Execute](../xml-elements-methods-execute.md) Analysis Services 인스턴스에서 개체를 만드는 방법.|  
|[Delete 요소](delete-element-xmla.md)|Analysis Services 인스턴스에서 개체를 삭제합니다.|  
|[DesignAggregations 요소](designaggregations-element-xmla.md)|Analysis Services 인스턴스에서 집계 디자인의 집계를 만듭니다.|  
|[Drop 요소](drop-element-xmla.md)|차원에서 특성 멤버를 삭제합니다.|  
|[Insert 요소](insert-element-xmla.md)|특성 멤버를 차원에 삽입합니다.|  
|[Lock 요소](lock-element-xmla.md)|Analysis Services 인스턴스에서 지정된 개체를 잠급니다.|  
|[MergePartitions 요소](mergepartitions-element-xmla.md)|하나 이상의 원본 파티션의 데이터를 대상 파티션에 병합한 다음 원본 파티션을 삭제합니다.|  
|[NotifyTableChange 요소](notifytablechange-element-xmla.md)|지정된 데이터 원본의 테이블이 변경되었음을 Analysis Services 인스턴스에 알립니다.|  
|[Process 요소](process-element-xmla.md)|Analysis Services 인스턴스에서 개체를 처리합니다.|  
|[Restore 요소](restore-element-xmla.md)|백업 파일에서 Analysis Services 데이터베이스를 복원합니다.|  
|[RollbackTransaction 요소](rollbacktransaction-element-xmla.md)|Analysis Services 인스턴스로 현재 세션에서 트랜잭션을 롤백합니다.|  
|[Statement 요소](statement-element-xmla.md)|Ccontains 쿼리 또는 문을 전송할를 사용 하는 [Execute](../xml-elements-methods-execute.md) Analysis Services 인스턴스에 메서드.|  
|[Subscribe 요소](subscribe-element-xmla.md)|추적에 대해 구독하고 Analysis Services 인스턴스의 추적 이벤트를 포함하는 행 집합을 반환합니다.|  
|[Synchronize 요소](synchronize-element-xmla.md)|Analysis Services 데이터베이스를 기존의 다른 데이터베이스와 동기화합니다.|  
|[Unlock 요소](unlock-element-xmla.md)|Analysis Services 인스턴스에서 지정된 잠금을 해제합니다.|  
|[Update 요소](../xml-elements-commands/update-element-xmla.md)|차원의 특성 멤버를 업데이트합니다.|  
|[UpdateCells 요소](updatecells-element-xmla.md)|쓰기 가능 큐브의 셀을 업데이트합니다.|  
  
  
