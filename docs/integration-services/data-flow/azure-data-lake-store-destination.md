---
description: Azure Data Lake Store 대상
title: Azure Data Lake Store 대상 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 55a30f509074401bcf940639e9e4df14d0a58add
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127348"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 대상

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Azure Data Lake Store 대상** 구성 요소를 사용하면 SSIS 패키지가 Azure Data Lake Store에 데이터를 쓸 수 있습니다. 지원되는 파일 형식은 다음과 같습니다. 텍스트, Avro 및 ORC. 
  
 **Azure Data Lake Store 대상** 은 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.
 
> [!NOTE]
> Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Azure Data Lake Store 원본과 Azure Data Lake Store 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 

**Azure Data Lake Store 대상 구성**

1. **Azure Data Lake Store 대상** 을 데이터 흐름 디자이너에 끌어서 놓은 다음 두 번 클릭하여 편집기를 표시합니다.  

2.  **Azure Data Lake Store 연결 관리자** 필드에서는 기존 Azure Data Lake Store 연결 관리자를 지정하거나 Azure Data Lake Store 서비스를 참조하는 연결 관리자를 새로 만듭니다.  
  
    1.  **파일 경로** 필드에서는 데이터를 기록할 파일 이름을 지정합니다. 이 파일이 이미 있는 경우 해당 콘텐츠를 덮어씁니다.  
  
    2.  **파일 형식** 필드에서는 사용할 파일 형식을 지정합니다.  
  
       파일 형식이 Text이면 **열 구분 기호 문자** 값을 지정해야 합니다. 파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.  

       파일 형식이 ORC 경우 Java가 필요 합니다. 자세한 내용은 [여기](../../integration-services/azure-feature-pack-for-integration-services-ssis.md#dependency-on-java)를 참조하세요.
  
3.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.  
