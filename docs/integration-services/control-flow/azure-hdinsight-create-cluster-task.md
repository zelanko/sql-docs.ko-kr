---
title: "Azure HDInsight 클러스터 만들기 태스크 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpcreatecltask.f1"
  - "sql14.dts.designer.afpcreatecltask.f1"
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Azure HDInsight 클러스터 만들기 태스크
  **Azure HDInsight 클러스터 만들기 태스크**를 사용하면 SSIS 패키지에서 지정된 Azure 구독에 Azure HDInsight 클러스터를 만들 수 있습니다.  
  
 **Azure HDInsight 클러스터 만들기 태스크**는 SQL Server 2016에 대해 제공되는 Azure용 SSIS(SQL Server Integration Services) 기능 팩의 구성 요소입니다. [여기](http://go.microsoft.com/fwlink/?LinkID=626967)서 기능 팩을 다운로드하세요.  
  
> [!NOTE]  
>  -   새 HDInsight 클러스터를 만들려면 일반적으로 10분이 걸립니다.  
> -   Azure HDInsight 클러스터 만들기 및 실행과 관련하여 비용은 발생하지 않습니다. 자세한 내용은 [HDInsight 가격](http://azure.microsoft.com/en-us/pricing/details/hdinsight/) 항목을 참조하세요.  
  
 **Azure HDInsight 클러스터 만들기 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집**을 클릭하여 다음과 같은 **Azure HDInsight 클러스터 만들기 태스크 편집기** 대화 상자를 표시합니다.  
  
 다음 표에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**Description**|  
|AzureSubscriptionConnection|기존 Azure 구독 연결 관리자를 선택하거나 HDInsight 클러스터를 호스트하는 Azure 구독을 참조하는 구독 연결 관리자를 새로 만듭니다.|  
|AzureStorageConnection|기존 Azure 저장소 연결 관리자를 선택하거나 HDInsight 클러스터에 연결할 Azure 저장소 계정을 참조하는 저장소 연결 관리자를 새로 만듭니다.|  
|위치|HDInsight 클러스터의 위치를 지정합니다. Azure 저장소와 동일한 위치에 클러스터를 만들어야 합니다.|  
|ClusterName|만들 HDInsight 클러스터의 이름을 지정합니다.|  
|ClusterSize|클러스터에 포함할 노드의 수를 지정합니다.|  
|BlobContainer|HDInsight 클러스터와 연결된 기본 저장소 컨테이너의 이름을 지정합니다.|  
|UserName|클러스터에 대한 액세스 권한이 있는 사용자의 이름을 지정합니다.|  
|암호|사용자의 암호를 지정합니다.|  
|FailIfExists|클러스터가 이미 있는 경우 태스크가 실패하는지 여부를 지정합니다.|  
  
> [!NOTE]  
>  HDInsight 클러스터와 Azure 저장소의 위치는 동일해야 합니다.  
  
  