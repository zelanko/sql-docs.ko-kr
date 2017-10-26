---
title: "Azure HDInsight 클러스터 삭제 작업 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f98b69e8bd3b2e78f6dd20a19ca17a83a834c3b3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight 클러스터 삭제 작업
**Azure HDInsight 클러스터 삭제 작업** SSIS 패키지는 지정된 된 Azure 구독 및 리소스 그룹에서 Azure HDInsight 클러스터를 삭제할 수 있습니다.
  
**Azure HDInsight 클러스터 삭제 작업** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.
  
> [!NOTE]
> HDInsight 클러스터 삭제에 10 걸릴 수 있습니다 ~ 20 분입니다.  
  
**Azure HDInsight 클러스터 삭제 작업**을 추가하려면 작업을 SSIS 디자이너로 끌어다 놓고 두 번 클릭하거나 **편집** 을 클릭하여 다음과 같은 **Azure HDInsight 클러스터 삭제 작업 편집기** 대화 상자를 표시합니다.  
  
다음 표에서 대화 상자에서 필드에 대 한 설명을 제공합니다.  
  
|||  
|-|-|  
|**필드**|**Description**|  
|AzureResourceManagerConnection|기존 Azure 리소스 관리자 연결 관리자를 선택 하거나 HDInsight 클러스터를 삭제 하는 데 사용할 새 이름을 만듭니다.|
|구독 Id|HDInsight 클러스터에는 구독 ID를 지정 합니다.|
|리소스 그룹|HDInsight 클러스터에는 Azure 리소스 그룹을 지정 합니다.|
|ClusterName|삭제할 클러스터의 이름을 지정합니다.|  
|FailIfNotExists|클러스터가 없는 경우 작업이 실패하는지 여부를 지정합니다.|

