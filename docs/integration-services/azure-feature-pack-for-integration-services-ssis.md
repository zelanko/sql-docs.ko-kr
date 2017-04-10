---
title: "Integration Services에 대한 Azure 기능 팩(SSIS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.AZURE.F1"
  - "SQL14.SSIS.AZURE.F1"
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# Integration Services에 대한 Azure 기능 팩(SSIS)
  SQL Server 2016에 대한 Azure용 SSIS(SQL Server Integration Services) 기능 팩은 Azure에 연결하고, Azure 및 온-프레미스 데이터 원본 간에 데이터를 전송하고, Azure에 저장된 데이터를 처리하기 위해 SSIS에 다음 구성 요소를 제공하는 확장 프로그램입니다.

[![Azure용 SSIS 기능 팩 다운로드](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=626967) **SQL Server 2016에 대한 Azure용 SSIS 기능 팩**  [다운로드](http://go.microsoft.com/fwlink/?LinkID=626967)


-   연결 관리자

    -   [Azure Storage 연결 관리자](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure 구독 연결 관리자](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
    -   [Azure Data Lake Store 연결 관리자](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

-   태스크

    -   [Azure Blob 업로드 태스크](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Blob 다운로드 작업](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure HDInsight 하이브 태스크](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig 태스크](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure HDInsight 클러스터 만들기 태스크](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight 클러스터 삭제 작업](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 업로드 태스크](../integration-services/control-flow/azure-sql-dw-upload-task.md)

-   데이터 흐름 구성 요소

    -   [Azure Blob 원본](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob 대상](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store 원본](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 대상](../integration-services/data-flow/azure-data-lake-store-destination.md)

-   Azure Blob 열거자. [열거자 = Foreach Azure Blob 열거자](../../../Topic/Foreach%20Loop%20Editor%20\(Collection%20Page\).md#ForeachAzureBlob)

## <a name="download-the-feature-pack"></a>기능 팩 다운로드
 [여기](http://go.microsoft.com/fwlink/?LinkID=626967)에서 SQL Server 2016에 대한 Azure용 SSIS(SQL Server Integration Services) 기능 팩을 다운로드합니다.

## <a name="prerequisites"></a>필수 구성 요소
 이 기능 팩을 설치하기 전에 다음과 같은 필수 조건을 설치해야 합니다.

-   SQL Server Integration Services

-   .Net Framework 4.5

## <a name="scenario-processing-big-data"></a>시나리오: 빅 데이터 처리
 Azure 커넥터를 사용하여 다음과 같은 빅 데이터 처리 작업을 완료합니다.

1.  Azure Blob 업로드 태스크를 사용하여 Azure Blob 저장소에 입력 데이터를 업로드합니다.

2.  Azure HDInsight 클러스터 만들기 태스크를 사용하여 Azure HDInsight 클러스터를 만듭니다. 자체 클러스터를 사용하려는 경우 이 단계는 선택 사항입니다.

3.  Azure HDInsight Hive 태스크 또는 Azure HDInsight Pig 태스크를 사용하여 Azure HDInsight 클러스터에서 Pig 또는 Hive 작업을 호출합니다.

4.  2단계에서 주문형 HDInsight 클러스터를 만든 경우 Azure HDInsight 클러스터 삭제 태스크를 사용하여 사용한 HDInsight 클러스터를 삭제합니다.

5.  Azure HDInsight Blob 다운로드 태스크를 사용하여 Azure Blob 저장소에서 Pig/Hive 출력 데이터를 다운로드합니다.

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>시나리오: 클라우드의 데이터 관리
 SSIS 패키지의 Azure Blob 대상을 사용하여 Azure Blob 저장소에 출력 데이터를 쓰거나 Azure Blob 원본을 사용하여 Azure Blob 저장소에서 데이터를 읽습니다.

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Azure Blob 열거자에서 Foreach 루프 컨테이너를 사용하여 다중 blob 파일의 데이터를 처리합니다.

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  