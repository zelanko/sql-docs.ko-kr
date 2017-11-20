---
title: "Azure 데이터 레이크 저장소 대상 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5f8cfa5230a36a27a7e98fa6f336bcee56fa062e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 대상
  **Azure Data Lake Store 대상** 구성 요소를 사용하면 SSIS 패키지가 Azure Data Lake Store에 데이터를 쓸 수 있습니다. 지원되는 파일 형식은 텍스트, Avro 및 ORC입니다. 
  
 **Azure 데이터 레이크 저장소 대상을** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.
 
 >   [!NOTE]
 > Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Azure Data Lake Store 원본과 Azure Data Lake Store 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 

## <a name="configure-the-azure-data-lake-store-destination"></a>Azure Data Lake Store 대상 구성  
1. **Azure Data Lake Store 대상** 을 데이터 흐름 디자이너에 끌어서 놓은 다음 두 번 클릭하여 편집기를 표시합니다.  

2.  **Azure Data Lake Store 연결 관리자** 필드에서는 기존 Azure Data Lake Store 연결 관리자를 지정하거나 Azure Data Lake Store 서비스를 참조하는 연결 관리자를 새로 만듭니다.  
  
    1.  **파일 경로** 필드에서는 데이터를 기록할 파일 이름을 지정합니다. 이 파일이 이미 있는 경우 해당 콘텐츠를 덮어쓰게 됩니다.  
  
    2.  **파일 형식** 필드에서는 사용할 파일 형식을 지정합니다.  
  
        파일 형식이 Text이면 **열 구분 기호 문자** 값을 지정해야 합니다. 파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.  

        파일 형식이 ORC이면 해당 플랫폼의 JRE를 설치해야 합니다. 
  
3.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.  
  
  

