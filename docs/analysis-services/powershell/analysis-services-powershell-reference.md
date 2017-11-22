---
title: "Analysis Services PowerShell 참조 | Microsoft Docs"
ms.custom: 
ms.date: 06/21/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8f23632c4b4dde2943d74a40e7ea0c75de963a4b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="analysis-services-powershell-reference"></a>Analysis Services PowerShell 참조

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]


  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]PowerShell cmdlet에 포함 된는 [SqlServer 모듈](https://www.powershellgallery.com/packages/SqlServer/21.0.17099)합니다. 
  
>[!NOTE] 
> Azure Analysis Services 데이터베이스 작업으로 SQL Server Analysis Services는 동일한 SqlServer 모듈을 사용합니다. 그러나 일부 cmdlet은 Azure Analysis Services에 대 한 지원 됩니다. 자세한 내용은 참고 [PowerShell과 함께 Azure Analysis Services 관리](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell)합니다.
  
##  <a name="bkmk_cmdlets"></a> Analysis Services Cmdlet  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 은 **Microsoft.AnalysisServices** 네임스페이스에서 메서드에 해당하는 cmdlet을 제공합니다. 다음 표에서는 각 cmdlet에 대해 설명하고 해당 AMO 메서드에 대한 링크를 제공합니다.  
  
 PowerShell을 사용하여 다음 목록에 없는 태스크(예: 데이터베이스 만들기 또는 동기화)를 수행하려는 경우 해당 작업에 대한 TMSL 또는 XMLA 스크립트를 작성한 다음 **Invoke-ASCmd** cmdlet을 사용하여 스크립트를 실행하면 됩니다.  
  
|Cmdlet|Description|동일한 AMO 메서드|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)|데이터베이스 역할에 멤버 추가|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Analysis Services 데이터베이스 백업|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|XMLA 또는 TSML(JSON) 형식으로 쿼리 또는 스크립트 실행|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|데이터베이스 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|큐브 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|차원 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|파티션 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|테이블 형식 모델, 호환성 모델 1200 이상에서 테이블을 처리 합니다.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)|파티션 병합|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|데이터베이스 백업을 포함할 폴더를 만듭니다.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|데이터베이스를 복원할 하나 이상의 원격 서버를 지정합니다.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|데이터베이스 역할에서 멤버 제거|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|서버 인스턴스에서 데이터베이스 복원|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
