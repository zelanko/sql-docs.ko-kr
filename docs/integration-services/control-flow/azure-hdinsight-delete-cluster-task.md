---
title: Azure HDInsight 클러스터 삭제 작업 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: db5a4a528313da8470d4e3a536c670ab268c0b6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight 클러스터 삭제 작업
**Azure HDInsight 클러스터 삭제 작업**을 사용하면 SSIS 패키지에서 지정된 Azure 구독 및 리소스 그룹의 Azure HDInsight 클러스터를 삭제할 수 있습니다.
  
**Azure HDInsight 클러스터 삭제 작업**은 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.
  
> [!NOTE]
> HDInsight 클러스터 삭제에는 10~20분이 걸립니다.  
  
**Azure HDInsight 클러스터 삭제 작업**을 추가하려면 작업을 SSIS 디자이너로 끌어다 놓고 두 번 클릭하거나 **편집** 을 클릭하여 다음과 같은 **Azure HDInsight 클러스터 삭제 작업 편집기** 대화 상자를 표시합니다.  
  
다음 표에서는 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**설명**|  
|AzureResourceManagerConnection|기존 Azure Resource Manager 연결 관리자를 선택하거나 HDInsight 클러스터를 삭제하는 데 사용할 새 연결 관리자를 만듭니다.|
|SubscriptionId|HDInsight 클러스터가 있는 구독 ID를 지정합니다.|
|ResourceGroup|HDInsight 클러스터가 있는 Azure 리소스 그룹을 지정합니다.|
|ClusterName|삭제할 클러스터의 이름을 지정합니다.|  
|FailIfNotExists|클러스터가 없는 경우 작업이 실패하는지 여부를 지정합니다.|
