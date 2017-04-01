---
title: "Azure HDInsight Pig 태스크 | Microsoft Docs"
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
  - "sql13.dts.designer.afppigtask.f1"
  - "sql14.dts.designer.afppigtask.f1"
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Azure HDInsight Pig 태스크
  **Azure HDInsight Pig 태스크** 를 사용하여 Azure HDInsight 클러스터에서 Pig 스크립트를 실행합니다. 
    
**Azure HDInsight Pig 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집**을 클릭하여 다음과 같은 **Azure HDInsight Pig 태스크 편집기** 대화 상자를 표시합니다.  
  
 **Azure HDInsight Pig 태스크**는 SQL Server 2016에 대해 제공되는 Azure용 SSIS(SQL Server Integration Services) 기능 팩의 구성 요소입니다. [여기](http://go.microsoft.com/fwlink/?LinkID=626967)서 기능 팩을 다운로드하세요.  
  
1.  **AzureSubscriptionConnection** 필드에서는 기존 Azure 구독 연결 관리자를 선택하거나 HDInsight 클러스터를 호스트하는 Azure 구독을 참조하는 구독 연결 관리자를 새로 만듭니다.  
  
2.  **HDInsightClusterName** 필드에는 Pig 스크립트를 실행할 HDInsight 클러스터의 이름을 입력합니다.  
  
3.  **LocalLogFolder** 필드에서는 **...(줄임표)**를 클릭하고 HDInsight 클러스터에서 Pig 처리 로그를 다운로드할 폴더를 선택합니다.  
  
4.  두 가지 방법으로 Pig 스크립트를 지정할 수 있습니다.  
  
    1.  **인라인 스크립트**: **스크립트** 필드 옆의 **...(줄임표)**를 클릭하고 **입력 스크립트** 대화 상자에 인라인 스크립트를 입력합니다.  
  
    2.  **스크립트 파일**: Blob 위치에 스크립트 파일을 업로드하고 해당 **BlobName**을 지정합니다. blob이 HDInsight 클러스터의 컨테이너 또는 기본 저장소에 Blob이 없으면 **ExternalStorageAccountName** 및 **ExternalBlobContainer** 를 지정해야 합니다. 외부 Blob의 경우에는 공용 액세스가 가능하도록 구성해야 합니다.  
  
     스크립트 파일과 인라인 스크립트를 모두 지정하면 스크립트 파일이 사용되며 인라인 스크립트는 무시됩니다.  
  
  