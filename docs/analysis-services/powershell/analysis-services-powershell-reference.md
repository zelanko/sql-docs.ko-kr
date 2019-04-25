---
title: Analysis Services PowerShell 참조 | Microsoft Docs
ms.date: 06/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13ea15a23bbf6de6c50b494f709f65cae2f7c48b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509843"
---
# <a name="analysis-services-powershell-reference"></a>Analysis Services PowerShell 참조
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell cmdlet이 포함 되어는 [SqlServer 모듈](https://www.powershellgallery.com/packages/SqlServer/21.0.17099)합니다. 
  
>[!NOTE] 
> SQL Server Analysis Services와 동일한 SqlServer 모듈을 사용 하는 azure Analysis Services 데이터베이스 작업입니다. 그러나 일부 cmdlet은 Azure Analysis Services에 대 한 지원 됩니다. 자세한 내용은 참조 하세요 [PowerShell 사용 하 여 Azure Analysis Services 관리](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell)합니다.
  
##  <a name="bkmk_cmdlets"></a> Analysis Services Cmdlet  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 은 **Microsoft.AnalysisServices** 네임스페이스에서 메서드에 해당하는 cmdlet을 제공합니다. 다음 표에서는 각 cmdlet에 대해 설명하고 해당 AMO 메서드에 대한 링크를 제공합니다.  
  
 PowerShell을 사용하여 다음 목록에 없는 태스크(예: 데이터베이스 만들기 또는 동기화)를 수행하려는 경우 해당 작업에 대한 TMSL 또는 XMLA 스크립트를 작성한 다음 **Invoke-ASCmd** cmdlet을 사용하여 스크립트를 실행하면 됩니다.  
  
|Cmdlet|Description|동일한 AMO 메서드|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/Add-RoleMember)|데이터베이스 역할에 멤버 추가|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/backup-asdatabase)|Analysis Services 데이터베이스 백업|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Invoke-ASCmd cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-ascmd)|XMLA 또는 TSML(JSON) 형식으로 쿼리 또는 스크립트 실행|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processasdatabase)|데이터베이스 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processcube)|큐브 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processdimension)|차원 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processpartition)|파티션 처리|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processtable)|호환성 모델 1200 이상인 테이블 형식 모델에서 테이블을 처리 합니다.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/merge-partition)|파티션 병합|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/new-restorefolder)|데이터베이스 백업을 포함할 폴더를 만듭니다.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/new-restorelocation)|데이터베이스를 복원할 하나 이상의 원격 서버를 지정합니다.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/remove-rolemember)|데이터베이스 역할에서 멤버 제거|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/restore-asdatabase)|서버 인스턴스에서 데이터베이스 복원|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
