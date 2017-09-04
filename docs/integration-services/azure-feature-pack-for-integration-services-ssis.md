---
title: "Integration Services (SSIS)에 대 한 azure 기능 팩 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4941d8eb846e9d47b008447fe0e346d43de5d87f
ms.openlocfilehash: d4204ba56e515025bed3ae3bf8e7a77d6da471be
ms.contentlocale: ko-kr
ms.lasthandoff: 08/30/2017

---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Integration Services에 대한 Azure 기능 팩(SSIS)
Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩에는 Azure 서비스, Azure 및 온-프레미스 데이터 원본 및 Azure에 저장 된 데이터 처리 간에 데이터를 전송에 연결 하는 SSIS 용이 페이지에 나열 된 구성 요소를 제공 하는 확장입니다.

[![Azure 용 SSIS 기능 팩 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=54798) **다운로드**

- SQL server 2017- [Microsoft SQL Server 2017 Integration Services 용 Azure 기능 팩](https://www.microsoft.com/download/details.aspx?id=54798)
- SQL server 2016- [Microsoft SQL Server 2016 Integration Services 용 Azure 기능 팩](https://www.microsoft.com/download/details.aspx?id=49492)
- SQL server 2014- [Microsoft SQL Server 2014 Integration Services 용 Azure 기능 팩](https://www.microsoft.com/en-us/download/details.aspx?id=47366)
- SQL server 2012- [Microsoft SQL Server 2012 Integration Services 용 Azure 기능 팩](https://www.microsoft.com/en-us/download/details.aspx?id=47367)

## <a name="components-in-the-feature-pack"></a>기능 팩의 구성 요소
-   연결 관리자

    -   [Azure Storage 연결 관리자](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure 구독 연결 관리자](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
    -   [Azure Data Lake Store 연결 관리자](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure 리소스 관리자 연결 관리자](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight 연결 관리자](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

-   태스크

    -   [Azure Blob 업로드 태스크](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Blob 다운로드 작업](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure HDInsight 하이브 태스크](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig 태스크](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure HDInsight 클러스터 만들기 태스크](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight 클러스터 삭제 작업](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 업로드 태스크](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Azure 데이터 레이크 저장소 파일 시스템 태스크](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

-   데이터 흐름 구성 요소

    -   [Azure Blob 원본](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob 대상](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store 원본](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 대상](../integration-services/data-flow/azure-data-lake-store-destination.md)

-   Azure Blob 및 ADLS File 열거자를 제공 합니다. 참조 [Foreach 루프 컨테이너](http://msdn.microsoft.com/library/95a19dde-61ca-4d9b-aa3d-131fa4264296)

## <a name="download-the-feature-pack"></a>기능 팩 다운로드
 Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩을 다운로드 합니다.
 
- [SSIS 용 기능 팩 Azure](http://go.microsoft.com/fwlink/?LinkID=626967) SQL Server 2016 용
- [SSIS 용 기능 팩 Azure](https://www.microsoft.com/en-us/download/details.aspx?id=54798) 에 대 한[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

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
  

