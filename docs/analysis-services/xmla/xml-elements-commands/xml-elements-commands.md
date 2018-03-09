---
title: "명령 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3ffde9e4cc1500ee0637225dc76153f3d81b463f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="xml-elements---commands"></a>XML 요소-명령
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]이 참조 섹션 내에서 사용할 수 있는 Analysis (XMLA) 요소에 대 한 XML이 포함 되어는 **명령** 중 요소는 **Execute** 메서드를 호출 합니다.  
  
|요소|Description|  
|-------------|-----------------|  
|[Alter 요소(XMLA)](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)|사용 하는 Analysis Services Scripting Language (ASSL) 요소를 포함 된 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 개체의 인스턴스를 변경 하려면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|[Backup 요소](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|백업 하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 백업 파일입니다.|  
|[일괄 처리 요소](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|순차 또는 병렬의 인스턴스에서 Analysis (XMLA) 명령에 대 한 하나 이상의 XML을 일괄 처리 작업으로 수행 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|[BeginTransaction 요소](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)|Analysis Services 인스턴스로 현재 세션에서 트랜잭션을 시작합니다.|  
|[Cancel 요소](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|Analysis Services 인스턴스에서 현재 실행 중인 명령을 취소합니다.|  
|[ClearCache 요소](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)|Analysis Services 인스턴스에서 지정된 개체의 메모리 캐시를 지웁니다.|  
|[CommitTransaction 요소](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)|Analysis Services 인스턴스로 현재 세션에서 트랜잭션을 커밋합니다.|  
|[Create 요소](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|사용 하는 Analysis Services Scripting Language (ASSL) 요소를 포함는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 방법을 Analysis Services 인스턴스에서 개체를 만들 수 있습니다.|  
|[Delete 요소](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)|Analysis Services 인스턴스에서 개체를 삭제합니다.|  
|[DesignAggregations 요소](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|Analysis Services 인스턴스에서 집계 디자인의 집계를 만듭니다.|  
|[Drop 요소](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|차원에서 특성 멤버를 삭제합니다.|  
|[Insert 요소](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)|특성 멤버를 차원에 삽입합니다.|  
|[Lock 요소](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)|Analysis Services 인스턴스에서 지정된 개체를 잠급니다.|  
|[MergePartitions 요소](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|하나 이상의 원본 파티션의 데이터를 대상 파티션에 병합한 다음 원본 파티션을 삭제합니다.|  
|[NotifyTableChange 요소](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|지정된 데이터 원본의 테이블이 변경되었음을 Analysis Services 인스턴스에 알립니다.|  
|[Process 요소](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|Analysis Services 인스턴스에서 개체를 처리합니다.|  
|[Restore 요소](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|백업 파일에서 Analysis Services 데이터베이스를 복원합니다.|  
|[RollbackTransaction 요소](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)|Analysis Services 인스턴스로 현재 세션에서 트랜잭션을 롤백합니다.|  
|[Statement 요소](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Ccontains 쿼리 또는 문을 보낼를 사용 하는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Analysis Services의 인스턴스로 메서드.|  
|[Subscribe 요소](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)|추적에 대해 구독하고 Analysis Services 인스턴스의 추적 이벤트를 포함하는 행 집합을 반환합니다.|  
|[Synchronize 요소](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|Analysis Services 데이터베이스를 기존의 다른 데이터베이스와 동기화합니다.|  
|[Unlock 요소](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|Analysis Services 인스턴스에서 지정된 잠금을 해제합니다.|  
|[Update 요소](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|차원의 특성 멤버를 업데이트합니다.|  
|[UpdateCells 요소](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|쓰기 가능 큐브의 셀을 업데이트합니다.|  
  
  
