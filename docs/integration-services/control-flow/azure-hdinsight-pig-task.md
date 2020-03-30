---
title: Azure HDInsight Pig 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 44d6fd9052b2f36381b95223222ec9008a8e4728
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298409"
---
# <a name="azure-hdinsight-pig-task"></a>Azure HDInsight Pig 태스크

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


**Azure HDInsight Pig 태스크** 를 사용하여 Azure HDInsight 클러스터에서 Pig 스크립트를 실행합니다.
     
**Azure HDInsight Pig 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 다음과 같은 **Azure HDInsight Pig 태스크 편집기** 대화 상자를 표시합니다.  
  
**Azure HDInsight Pig 태스크**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.
  
 다음 목록에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
1.  **HDInsightConnection** 필드에서는 기존 Azure HDInsight 연결 관리자를 선택하거나 스크립트를 실행하는 데 사용한 Azure HDInsight 클러스터를 참조하는 HDInsight 연결 관리자를 새로 만듭니다.
  
2.  **AzureStorageConnection** 필드에서는 기존 Azure Storage 연결 관리자를 선택하거나 클러스터에 연결된 Azure Storage 계정을 참조하는 Storage 연결 관리자를 새로 만듭니다. 스크립트 실행 출력 및 오류 로그를 다운로드하려는 경우에만 필요합니다.
 
3.  **BlobContainer** 필드의 경우 클러스터와 연결된 스토리지 컨테이너 이름을 지정합니다. 스크립트 실행 출력 및 오류 로그를 다운로드하려는 경우에만 필요합니다.
  
4.  **LocalLogFolder** 필드의 경우 스크립트 실행 출력 및 오류 로그를 다운로드할 폴더를 지정합니다. 스크립트 실행 출력 및 오류 로그를 다운로드하려는 경우에만 필요합니다.   
  
5.  두 가지 방법으로 실행할 Pig 스크립트를 지정할 수 있습니다.
  
    1.  **인라인 스크립트**: **스크립트 입력** 대화 상자에 실행할 인라인 스크립트를 입력하여 **스크립트** 필드를 지정합니다.
  
    2.  **스크립트 파일**: Azure Blob Storage에 스크립트 파일을 업로드하고 **BlobName** 필드를 지정합니다. blob이 기본 스토리지 계정 또는 HDInsight 클러스터와 연결된 컨테이너에 없는 경우 **ExternalStorageAccountName** 및 **ExternalBlobContainer** 필드를 지정해야 합니다. 외부 Blob의 경우에는 공용으로 액세스할 수 있도록 구성해야 합니다.  
  
     스크립트 파일과 인라인 스크립트를 모두 지정하면 스크립트 파일이 사용되며 인라인 스크립트는 무시됩니다.
