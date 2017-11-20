---
title: "Azure HDInsight 하이브 태스크 | Microsoft Docs"
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
- sql13.dts.designer.afphivetask.f1
- sql14.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f9e67e91b5cd38482ab1151d5942c9c55c04136c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-hive-task"></a>Azure HDInsight 하이브 태스크
**Azure HDInsight 하이브 태스크** 를 사용하여 Azure HDInsight 클러스터에서 하이브 스크립트를 실행합니다.
     
**Azure HDInsight 하이브 태스크**를 추가하려면 해당 태스크를 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 다음과 같은 **Azure HDInsight 하이브 태스크 편집기** 대화 상자를 표시합니다.  
  
**Azure HDInsight 하이브 태스크** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.
  
 다음 목록에서는 이 대화 상자의 필드에 대해 설명합니다.  
  
1.  에 대 한는 **HDInsightConnection** 필드에서는 기존 Azure HDInsight 연결 관리자를 선택 하거나 새 스크립트를 실행 하는 데 Azure HDInsight 클러스터를 가리키는 하나 만듭니다.
  
2.  에 대 한는 **AzureStorageConnection** 필드에서는 기존 Azure 저장소 연결 관리자를 선택 하거나 새 클러스터와 연결 된 Azure 저장소 계정을 참조 하는 하나 만듭니다. 이 스크립트 실행 출력 및 오류 로그를 다운로드 하려는 경우 필요만 합니다.
 
3.  에 대 한는 **BlobContainer** 필드는 클러스터와 연결 된 저장소 컨테이너 이름을 지정 합니다. 이 스크립트 실행 출력 및 오류 로그를 다운로드 하려는 경우 필요만 합니다.
  
4.  에 대 한는 **LocalLogFolder** 필드는 있는 스크립트 실행 출력 및 오류 로그를 다운로드할 폴더를 지정 합니다. 이 스크립트 실행 출력 및 오류 로그를 다운로드 하려는 경우 필요만 합니다.   
  
5.  두 가지 방법으로 하이브 스크립트를 실행할 수를 지정할 수 있습니다.
  
    1.  **인라인 스크립트**: 지정 된 **스크립트** 필드를 입력 하 여 인라인 스크립트에서를 실행 하는 **입력 스크립트** 대화 상자.
  
    2.  **스크립트 파일**: Azure Blob 저장소에 스크립트 파일을 업로드 하 고 지정 된 **BlobName** 필드입니다. Blob HDInsight 클러스터와 연결 된 컨테이너 또는 기본 저장소 계정에 없는 경우는 **ExternalStorageAccountName** 및 **ExternalBlobContainer** 필드를 지정 해야 합니다. 외부 blob의 경우에 대 한 구성 되어 있는지 같이 공개적으로 액세스할 수 있도록 합니다.  
  
     둘 다 지정 하면 스크립트 파일을 사용 하 고 인라인 스크립트가 무시 됩니다.

