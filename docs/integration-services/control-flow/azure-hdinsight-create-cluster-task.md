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
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 71a24dc15253916c32b07e6024e2ab32514c9d39
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight 클러스터 만들기 태스크
**Azure HDInsight 클러스터 만들기 태스크** 는 SSIS 패키지가 지정된 된 Azure 구독 및 리소스 그룹에서 Azure HDInsight 클러스터를 만들 수 있습니다.
  
**Azure HDInsight 클러스터 만들기 태스크** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.
  
> [!NOTE]  
> - 새 HDInsight 클러스터를 만드는 데 10 걸릴 수 있습니다 ~ 20 분입니다.  
> - 만들기 및 실행 하는 Azure HDInsight 클러스터와 관련 된 비용이 듭니다. 참조 [HDInsight 가격](http://azure.microsoft.com/en-us/pricing/details/hdinsight/) 대 한 자세한 내용은 합니다.  
  
**Azure HDInsight 클러스터 만들기 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 다음과 같은 **Azure HDInsight 클러스터 만들기 태스크 편집기** 대화 상자를 표시합니다.  
  
다음 표에서이 대화 상자에 있는 필드에 대 한 설명을 제공합니다.  
  
|||  
|-|-|  
|**필드**|**Description**|  
|AzureResourceManagerConnection|기존 Azure 리소스 관리자 연결 관리자를 선택 하거나 HDInsight 클러스터를 만드는 데 사용할 새 이름을 만듭니다.|  
|AzureStorageConnection|기존 Azure 저장소 연결 관리자를 선택하거나 HDInsight 클러스터에 연결할 Azure 저장소 계정을 참조하는 저장소 연결 관리자를 새로 만듭니다.|
|구독 Id|HDInsight 클러스터를 만들 구독의 ID를 지정 합니다.|
|리소스 그룹|Azure 리소스 그룹에 클러스터를 만들 HDInsight를 지정 합니다.|
|위치|HDInsight 클러스터의 위치를 지정합니다. 지정 된 Azure 저장소 계정과 동일한 위치에 클러스터를 만들어야 합니다.|  
|ClusterName|만들 HDInsight 클러스터의 이름을 지정합니다.|  
|ClusterSize|클러스터에서 만드는 노드 수를 지정 합니다.|  
|BlobContainer|HDInsight 클러스터와 연결할 기본 저장소 컨테이너의 이름을 지정 합니다.|  
|UserName|HDInsight 클러스터에 연결 하는 데 사용할 사용자 이름을 지정 합니다.|  
|암호|HDInsight 클러스터에 연결 하는 데 사용할 암호를 지정 합니다.|
|SshUserName|SSH를 사용 하 여 HDInsight 클러스터에 원격으로 액세스 하는 데 사용 사용자 이름을 지정 합니다.|
|SshPassword|SSH를 사용 하 여 HDInsight 클러스터에 원격으로 액세스 하는 데 사용 되는 암호를 지정 합니다.|
|FailIfExists|클러스터가 이미 있는 경우 태스크가 실패하는지 여부를 지정합니다.|  
  
> [!NOTE]  
> Azure 저장소 계정 및 HDInsight 클러스터의 위치는 동일 해야 합니다.

