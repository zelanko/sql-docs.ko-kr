---
title: Azure Data Lake Store 원본 | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8f37ede2738d9fd9da71b0b1e34411a099a42cbb
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58281507"
---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store 원본
  **Azure Data Lake Store 원본** 구성 요소를 사용하면 SSIS 패키지가 Azure Data Lake Store에서 데이터를 읽을 수 있습니다. 지원되는 파일 형식은 다음과 같습니다. 텍스트 및 Avro.
  
 **Azure Data Lake Store 원본**은 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.  
  
> [!NOTE]
> Azure Data Lake Store 연결 관리자와 이 연결 관리자를 사용하는 구성 요소(즉, Azure Data Lake Store 원본과 Azure Data Lake Store 대상)를 서비스에 연결하려면 [여기](https://www.microsoft.com/download/details.aspx?id=49492)에서 최신 버전의 Azure 기능 팩을 다운로드하세요. 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Azure Data Lake Store 원본 구성
 1. Azure Data Lake Store 원본용 편집기를 표시하려면 데이터 흐름 디자이너에서 **Azure Data Lake Store 원본** 을 끌어서 놓고 두 번 클릭하여 편집기를 엽니다.  
  
2.  **Azure Data Lake Store 연결 관리자** 필드에서는 기존 Azure Data Lake Store 연결 관리자를 지정하거나 Azure Data Lake Store 서비스를 참조하는 연결 관리자를 새로 만듭니다.  
  
    1.  **파일 경로** 필드에서는 Azure Data Lake Store에 있는 원본 파일의 파일 경로를 지정합니다.   
  
    2.  **파일 형식** 필드에서는 원본 파일의 파일 형식을 지정합니다.  
  
        파일 형식이 Text이면 **열 구분 기호 문자** 값을 지정해야 합니다. 파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.  
  
3.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.   

## <a name="text-qualifier"></a>텍스트 한정자

**Azure Data Lake Store 원본**은 텍스트 한정자를 지원하지 않습니다. 파일을 올바르게 처리하도록 텍스트 한정자를 지정해야 하는 경우 로컬 컴퓨터에 파일을 다운로드하고 **플랫 파일 원본**을 사용하여 파일을 처리하는 것이 좋습니다. 플랫 파일 원본을 통해 텍스트 한정자를 지정할 수 있습니다. 자세한 내용은 [플랫 파일 원본](flat-file-source.md)을 참조하세요.
