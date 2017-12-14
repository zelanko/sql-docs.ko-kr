---
title: "Azure HDInsight 클러스터 만들기 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe1114d05dc9eb31f3cec4c655bc2ae244683877
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight 클러스터 만들기 태스크
**Azure HDInsight 클러스터 만들기 태스크** 를 사용하면 SSIS 패키지에서 지정된 Azure 구독 및 리소스 그룹에 Azure HDInsight 클러스터를 만들 수 있습니다.
  
**Azure HDInsight 클러스터 만들기 태스크**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.
  
> [!NOTE]  
> - 새 HDInsight 클러스터 만들기에는 10~20분이 걸립니다.  
> - Azure HDInsight 클러스터 만들기 및 실행과 관련하여 비용이 듭니다. 자세한 내용은 [HDInsight 가격 책정](http://azure.microsoft.com/en-us/pricing/details/hdinsight/)을 참조하세요.  
  
**Azure HDInsight 클러스터 만들기 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 다음과 같은 **Azure HDInsight 클러스터 만들기 태스크 편집기** 대화 상자를 표시합니다.  
  
다음 표에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**Description**|  
|AzureResourceManagerConnection|기존 Azure Resource Manager 연결 관리자를 선택하거나 HDInsight 클러스터를 만드는 데 사용할 새 연결 관리자를 만듭니다.|  
|AzureStorageConnection|기존 Azure 저장소 연결 관리자를 선택하거나 HDInsight 클러스터에 연결할 Azure 저장소 계정을 참조하는 저장소 연결 관리자를 새로 만듭니다.|
|SubscriptionId|HDInsight 클러스터가 만들어질 구독 ID를 지정합니다.|
|ResourceGroup|HDInsight 클러스터가 만들어질 Azure 리소스 그룹을 지정합니다.|
|위치|HDInsight 클러스터의 위치를 지정합니다. Azure Storage 계정과 동일한 위치에 클러스터를 만들어야 합니다.|  
|ClusterName|만들 HDInsight 클러스터의 이름을 지정합니다.|  
|ClusterSize|클러스터에 만들 노드의 수를 지정합니다.|  
|BlobContainer|HDInsight 클러스터와 연결될 기본 저장소 컨테이너의 이름을 지정합니다.|  
|UserName|HDInsight 클러스터에 연결하는 데 사용할 사용자 이름을 지정합니다.|  
|암호|HDInsight 클러스터에 연결하는 데 사용할 암호를 지정합니다.|
|SshUserName|SSH를 사용하여 HDInsight 클러스터에 원격으로 액세스하는 데 사용할 사용자 이름을 지정합니다.|
|SshPassword|SSH를 사용하여 HDInsight 클러스터에 원격으로 액세스하는 데 사용할 암호를 지정합니다.|
|FailIfExists|클러스터가 이미 있는 경우 태스크가 실패하는지 여부를 지정합니다.|  
  
> [!NOTE]  
> HDInsight 클러스터와 Azure Storage 계정의 위치는 동일해야 합니다.
