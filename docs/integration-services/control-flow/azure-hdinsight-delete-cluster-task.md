---
title: "Azure HDInsight 클러스터 삭제 작업 | Microsoft Docs"
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
  - "sql13.dts.designer.afpdelcltask.f1"
  - "sql14.dts.designer.afpdelcltask.f1"
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Azure HDInsight 클러스터 삭제 작업
  **Azure HDInsight 클러스터 삭제 작업**을 사용하면 SSIS 패키지에서 지정된 Azure 구독의 Azure HDInsight 클러스터를 삭제할 수 있습니다.  
  
 **Azure HDInsight 클러스터 삭제 작업**은 SQL Server 2016에 대해 제공되는 Azure용 SSIS(SQL Server Integration Services) 기능 팩의 구성 요소입니다. [여기](http://go.microsoft.com/fwlink/?LinkID=626967)서 기능 팩을 다운로드하세요.  
  
> [!NOTE]  
>  HDInsight 클러스터 삭제에는 일반적으로 10분이 걸립니다.  
  
 **Azure HDInsight 클러스터 삭제 작업**을 추가하려면 작업을 SSIS 디자이너로 끌어다 놓고 두 번 클릭하거나 **편집**을 클릭하여 다음과 같은 **Azure HDInsight 클러스터 삭제 작업 편집기** 대화 상자를 표시합니다.  
  
 다음 표에서는 대화 상자의 필드에 대해 설명합니다.  
  
|||  
|-|-|  
|**필드**|**Description**|  
|AzureSubscriptionConnection|기존 Azure 구독 연결 관리자를 선택하거나 HDInsight 클러스터를 호스트하는 Azure 구독을 참조하는 구독 연결 관리자를 새로 만듭니다.|  
|ClusterName|삭제할 클러스터의 이름을 지정합니다.|  
|FailIfNotExists|클러스터가 없는 경우 작업이 실패하는지 여부를 지정합니다.|  
  
  