---
title: "Analysis Services PowerShell 참조 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Analysis Services PowerShell 참조
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에는 Windows PowerShell을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 탐색, 관리 및 쿼리할 수 있도록 PowerShell 공급자(SQLAS) 및 cmdlet(SQLASCMDLETS)이 포함되어 있습니다. 공급자 및 cmdlet을 로드하고 사용하는 방법은 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)을 참조하십시오. PowerShell에서 AMO 유형을 사용하여 테이블 형식 데이터베이스를 만드는 방법에 대한 예제는 [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md)을(를) 참조하세요.  
  
##  <a name="bkmk_cmdlets"></a> Analysis Services Cmdlet  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 은 **Microsoft.AnalysisServices** 네임스페이스에서 메서드에 해당하는 cmdlet을 제공합니다. 다음 표에서는 각 cmdlet에 대해 설명하고 해당 AMO 메서드에 대한 링크를 제공합니다.  
  
 PowerShell을 사용하여 다음 목록에 없는 태스크(예: 데이터베이스 만들기 또는 동기화)를 수행하려는 경우 해당 작업에 대한 TMSL 또는 XMLA 스크립트를 작성한 다음 **Invoke-ASCmd** cmdlet을 사용하여 스크립트를 실행하면 됩니다.  
  
|Cmdlet|Description|동일한 AMO 메서드|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)|데이터베이스 역할에 멤버 추가|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Analysis Services 데이터베이스 백업|<xref:Microsoft.AnalysisServices.Database.Backup%2A>|  
|[Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|XMLA 또는 TSML(JSON) 형식으로 쿼리 또는 스크립트 실행|<xref:Microsoft.AnalysisServices.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|데이터베이스 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|큐브 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|차원 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|파티션 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|테이블 형식 모델, 호환성 모델 1200 이상에서 테이블 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)|파티션 병합|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|데이터베이스 백업을 포함할 폴더를 만듭니다.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|데이터베이스를 복원할 하나 이상의 원격 서버를 지정합니다.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|데이터베이스 역할에서 멤버 제거|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|서버 인스턴스에서 데이터베이스 복원|<xref:Microsoft.AnalysisServices.Server.Restore%2A>|  
  
## 관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services Scripting Language&#40;XMLA용 ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)  
  
  