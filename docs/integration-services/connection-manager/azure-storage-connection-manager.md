---
title: "Azure 저장소 연결 관리자 | Microsoft Docs"
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
  - "sql13.dts.designer.afpstorageconn.f1"
  - "sql14.dts.designer.afpstorageconn.f1"
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Azure 저장소 연결 관리자
  SSIS 패키지는 **Azure 저장소 연결 관리자** 를 통해 속성으로 지정된 값(저장소 계정 이름 및 계정 키)을 사용하여 Azure 저장소 계정에 연결할 수 있습니다.  
  
>   [!NOTE] Azure Storage 연결 관리자 및 이를 사용하는 구성 요소(Blob 원본, Blob 대상, Blob 업로드 태스크 및 Blob 다운로드 태스크)에서 범용 저장소 계정과 Blob Storage 계정 모두에 연결할 수 있도록 하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure Feature Pack을 다운로드하세요. 이러한 두 가지 유형의 저장소 계정에 대한 자세한 내용은 [Microsoft Azure Storage 소개](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)를 참조하세요.
  
 **Azure Storage 연결 관리자**는 SQL Server 2016에 대해 제공되는 Azure용 SSIS(SQL Server Integration Services) 기능 팩의 구성 요소입니다. [여기](http://go.microsoft.com/fwlink/?LinkID=626967)서 기능 팩을 다운로드하세요.  
  
1.  **SSIS 연결 관리자 추가** 대화 상자에서 **AzureStorage**를 선택하고 **추가**를 클릭합니다.  
  
2.  Azure 저장소 연결 관리자 편집기 대화 상자에서 **Azure 계정 사용** 을 선택하여 인터넷을 통해 Azure 저장소 서비스에 연결하거나 **로컬 개발자 계정 사용** 을 선택하여 Azure 저장소 에뮬레이터가 호스트하는 로컬 서비스에 연결합니다.  
  
3.  **Azure 계정 사용** 옵션을 선택하는 경우 다음 단계를 수행합니다.  
  
    1.  **저장소 계정 이름** 및 **계정 키** 필드의 값을 지정합니다. 이러한 값은 SSIS 패키지에 중요한 데이터로 저장됩니다.  
  
    2.  HTTP 대신 HTTPS를 사용하여 Azure 저장소 서비스에 연결하려면 **HTTPS 사용** 을 선택합니다.  
  
4.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
5.  작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.  
  
  