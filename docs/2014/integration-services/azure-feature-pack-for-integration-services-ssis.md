---
title: Azure 기능 팩 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.SSIS.AZURE.F1
- SQL12.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 536dce64880c1e70b1b8a0c4b419811c1b32a975
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394529"
---
# <a name="azure-feature-pack"></a>Azure 기능 팩
Azure용 SSIS(SQL Server Integration Services) 기능 팩은 Azure 서비스에 연결하고, Azure 및 온-프레미스 데이터 원본 간에 데이터를 전송하고, Azure에 저장된 데이터를 처리하기 위해 SSIS에 이 페이지에 나열된 구성 요소를 제공하는 확장 프로그램입니다.

## <a name="components-in-the-feature-pack"></a>기능 팩의 구성 요소
  
-   연결 관리자  
  
    -   [Azure Storage 연결 관리자](connection-manager/azure-storage-connection-manager.md)  
  
    -   [Azure 구독 연결 관리자](connection-manager/azure-subscription-connection-manager.md)  
    
    -   [Azure Data Lake Store 연결 관리자](../../2014/integration-services/azure-data-lake-store-connection-manager.md)
    
    -   [Azure Resource Manager 연결 관리자](../../2014/integration-services/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight 연결 관리자](../../2014/integration-services/azure-hdinsight-connection-manager.md)
  
-   태스크  
  
    -   [Azure Blob 업로드 태스크](control-flow/azure-blob-upload-task.md)  
  
    -   [Azure Blob 다운로드 작업](control-flow/azure-blob-download-task.md)  
  
    -   [Azure HDInsight 하이브 태스크](control-flow/azure-hdinsight-hive-task.md)  
  
    -   [Azure HDInsight Pig 태스크](https://msdn.microsoft.com/library/mt146781(v=sql.120).aspx)
  
    -   [Azure HDInsight 클러스터 만들기 태스크](control-flow/azure-hdinsight-create-cluster-task.md)  
  
    -   [Azure HDInsight 클러스터 삭제 작업](control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 업로드 태스크](../../2014/integration-services/azure-sql-dw-upload-task.md)    
    
    -   [Azure Data Lake Store 파일 시스템 태스크](control-flow/file-system-task.md)    
  
-   데이터 흐름 구성 요소  
  
    -   [Azure Blob 원본](https://msdn.microsoft.com/library/mt146775(v=sql.120).aspx)  
  
    -   [Azure Blob 대상](data-flow/azure-blob-destination.md)  
    
    -   [Azure Data Lake Store 원본](../../2014/integration-services/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 대상](../../2014/integration-services/azure-data-lake-store-destination.md)
  
-   Azure Blob 열거자 및 ADLS File 열거자입니다. [Foreach Loop Container](control-flow/foreach-loop-container.md)을 참조하세요.  
  
 
## <a name="download-the-feature-pack"></a>기능 팩 다운로드  
Azure용 SSIS(SQL Server Integration Services) 기능 팩을 다운로드합니다.  
  
-   [Microsoft SQL Server 2014 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=47366)  

## <a name="prerequisites"></a>사전 요구 사항  
이 기능 팩을 설치하기 전에 다음과 같은 필수 조건을 설치해야 합니다.  
  
-   SQL Server Integration Services  
-   .Net Framework 4.5  
  
## <a name="scenarios"></a>시나리오  
  
### <a name="big-data-processing"></a>빅 데이터 처리  
 Azure 커넥터를 사용하여 다음과 같은 빅 데이터 처리 작업을 완료합니다.  
  
1.  Azure Blob 업로드 태스크를 사용하여 Azure Blob Storage에 입력 데이터를 업로드합니다.  
  
2.  Azure HDInsight 클러스터 만들기 태스크를 사용하여 Azure HDInsight 클러스터를 만듭니다. 자체 클러스터를 사용하려는 경우 이 단계는 선택 사항입니다.  
  
3.  Azure HDInsight Hive 태스크 또는 Azure HDInsight Pig 태스크를 사용하여 Azure HDInsight 클러스터에서 Pig 또는 Hive 작업을 호출합니다.  
  
4.  2단계에서 주문형 HDInsight 클러스터를 만든 경우 Azure HDInsight 클러스터 삭제 태스크를 사용하여 사용한 HDInsight 클러스터를 삭제합니다.  
  
5.  Azure HDInsight Blob 다운로드 태스크를 사용하여 Azure Blob Storage에서 Pig/Hive 출력 데이터를 다운로드합니다.  
  
 ![SSIS-AzureConnector-BigDataScenario](media/ssis-azureconnector-bigdatascenario.png "SSIS-AzureConnector-BigDataScenario")  
  
### <a name="cloud-data-archiving"></a>클라우드 데이터 보관  
 SSIS 패키지의 Azure Blob 대상을 사용하여 Azure Blob Storage에 출력 데이터를 쓰거나 Azure Blob 원본을 사용하여 Azure Blob Storage에서 데이터를 읽습니다.  
  
 ![SSIS-AzureConnector-CloudArchive-1](media/ssis-azureconnector-cloudarchive-1.png "SSIS-AzureConnector-CloudArchive-1")  
  
 ![SSIS-AzureConnector-CloudArchive-2](media/ssis-azureconnector-cloudarchive-2.png "SSIS-AzureConnector-CloudArchive-2")  
  
 또한 Azure Blob 열거자에서 Foreach 루프 컨테이너를 사용하여 다중 blob 파일의 데이터를 처리합니다.  
  
 ![SSIS-AzureConnector-CloudArchive-3](media/ssis-azureconnector-cloudarchive-3.png "SSIS-AzureConnector-CloudArchive-3")  
  
  
