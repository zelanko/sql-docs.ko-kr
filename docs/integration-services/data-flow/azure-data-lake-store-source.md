---
title: "Azure 데이터 레이크 저장소 소스 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 65b4526b4c83525f61d53807fd21c72de4ee087a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store 원본
  **Azure Data Lake Store 원본** 구성 요소를 사용하면 SSIS 패키지가 Azure Data Lake Store에서 데이터를 읽을 수 있습니다. 지원되는 파일 형식은 Text 및 Avro입니다.
  
 **Azure 데이터 레이크 저장소 소스** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.  
  
>   [!NOTE]
> Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Azure Data Lake Store 원본과 Azure Data Lake Store 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Azure Data Lake Store 원본 구성
 1. Azure Data Lake Store 원본용 편집기를 표시하려면 데이터 흐름 디자이너에서 **Azure Data Lake Store 원본** 을 끌어서 놓고 두 번 클릭하여 편집기를 엽니다.  
  
2.  **Azure Data Lake Store 연결 관리자** 필드에서는 기존 Azure Data Lake Store 연결 관리자를 지정하거나 Azure Data Lake Store 서비스를 참조하는 연결 관리자를 새로 만듭니다.  
  
    1.  **파일 경로** 필드에서는 Azure Data Lake Store에 있는 원본 파일의 파일 경로를 지정합니다.   
  
    2.  **파일 형식** 필드에서는 원본 파일의 파일 형식을 지정합니다.  
  
        파일 형식이 Text이면 **열 구분 기호 문자** 값을 지정해야 합니다. 파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.  
  
3.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.   
