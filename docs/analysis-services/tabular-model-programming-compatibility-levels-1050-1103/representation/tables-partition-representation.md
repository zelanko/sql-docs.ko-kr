---
title: "파티션 표현 (테이블 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: b606cd63-755c-4ac0-b19b-95b5363afbdf
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8a0509c571af328e4f5a459dbcbc68e1672d00f4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tables---partition-representation"></a>테이블-파티션 표현
  원활한 운영을 위해 테이블 하나를 여러 개의 행 하위 집합으로 나눌 수 있습니다. 이 행들이 결합하여 테이블을 구성하며 각각의 하위 집합은 테이블의 파티션입니다.  
  
## <a name="partition-representation"></a>파티션 표현  
 AMO 개체를 기준으로 파티션 표현은 <xref:Microsoft.AnalysisServices.Partition>과 일 대 일 매핑 관계를 가지며 그 밖의 주요 AMO 개체는 필수 항목이 아닙니다.  
  
### <a name="partition-in-amo"></a>AMO의 파티션  
 AMO를 사용하여 파티션을 관리하는 경우 테이블 형식 모델 테이블을 나타내는 측정값 그룹을 찾아서 해당 그룹에 대해 작업해야 합니다.  
  
 다음 코드 조각에서는 파티션을 기존 테이블 형식 모델 테이블에 추가하는 방법을 보여 줍니다.  
  
```  
  
private void AddPartition(  
                     AMO.Cube modelCube  
                  ,  AMO.DataSource newDatasource  
                  ,  string mgName  
                  ,  string newPartitionName  
                  , string partitionSelectStatement  
                  , Boolean processPartition  
             )  
{  
    mgName = mgName.Trim();  
    newPartitionName = newPartitionName.Trim();  
    partitionSelectStatement = partitionSelectStatement.Trim();  
    //Validate Input  
    if (string.IsNullOrEmpty(newPartitionName) || string.IsNullOrWhiteSpace(newPartitionName))  
    {  
        MessageBox.Show(String.Format("Partition Name cannot be empty or blank"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (modelCube.MeasureGroups[mgName].Partitions.ContainsName(newPartitionName))  
    {  
        MessageBox.Show(String.Format("Partition Name already defined. Duplicated names are not allowed"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (string.IsNullOrEmpty(partitionSelectStatement) || string.IsNullOrWhiteSpace(partitionSelectStatement))  
    {  
        MessageBox.Show(String.Format("Select statement cannot be empty or blank"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    //Input validated  
    string partitionID = newPartitionName; //Using partition name as the ID  
    AMO.Partition currentPartition = new AMO.Partition(partitionID, partitionID);  
    currentPartition.StorageMode = AMO.StorageMode.InMemory;  
    currentPartition.ProcessingMode = AMO.ProcessingMode.Regular;  
    currentPartition.Source = new AMO.QueryBinding(newDatasource.ID, partitionSelectStatement);  
    modelCube.MeasureGroups[mgName].Partitions.Add(currentPartition);  
    try  
    {  
        modelCube.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
        if (processPartition)  
        {  
            modelCube.MeasureGroups[mgName].Partitions[partitionID].Process(AMO.ProcessType.ProcessFull);  
            MessageBox.Show(String.Format("Partition successfully processed."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        }  
  
    }  
    catch (AMO.AmoException amoXp)  
    {  
        MessageBox.Show(String.Format("AMO exception accessing the server.\nError message: {0}", amoXp.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
    catch (Exception)  
    {  
        throw;  
    }  
}  
  
```  
  
## <a name="amo2tabular-sample"></a>AMO2Tabular 예제  
 그러나 AMO를 사용하여 파티션 표현을 만들고 조작하는 방법을 알아보려면 AMO to Tabular 예제의 원본 코드를 참조하십시오. 예제는 Codeplex에서 사용할 수 있습니다. 코드에 대한 중요 정보: 코드는 여기에서 설명한 논리적 개념에 대한 지원으로만 제공되며 프로덕션 환경에서 사용해서는 안 됩니다. 그리고 교육 목적 이외의 목적으로는 사용할 수 없습니다.  
  
  

