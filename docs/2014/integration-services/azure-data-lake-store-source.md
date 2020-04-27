---
title: Azure Data Lake Store 원본 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSSRC.F1
- SQL11.DTS.DESIGNER.AFPADLSSRC.F1
ms.assetid: 7d9e8457-62aa-4aea-98ee-7d1121dfae4f
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: 07ca2a75fa3f7e6329443bb4f71a23f52662f0f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061349"
---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store 원본
  **Azure Data Lake Store 원본** 구성 요소를 사용하면 SSIS 패키지가 Azure Data Lake Store에서 데이터를 읽을 수 있습니다. 지원되는 파일 형식은 Text 및 Avro입니다.
  
## <a name="configure-the-azure-data-lake-store-source"></a>Azure Data Lake Store 원본 구성 
  
1.  Azure Data Lake Store 원본용 편집기를 표시하려면 데이터 흐름 디자이너에서 **Azure Data Lake Store 원본** 을 끌어서 놓고 두 번 클릭하여 편집기를 엽니다.  
  
2.  **Azure Data Lake Store 연결 관리자** 필드에서는 기존 Azure Data Lake Store 연결 관리자를 지정하거나 Azure Data Lake Store 서비스를 참조하는 연결 관리자를 새로 만듭니다.  
  
    1.  **파일 경로** 필드에서는 Azure Data Lake Store에 있는 원본 파일의 파일 경로를 지정합니다.   
  
    2.  **파일 형식** 필드에서는 원본 파일의 파일 형식을 지정합니다.  
  
        파일 형식이 Text이면 **열 구분 기호 문자** 값을 지정해야 합니다. 또한 파일의 첫 번째 행에 열 이름이 포함 된 경우 **첫 번째 데이터 행에서 열 이름을** 선택 합니다.  
  
3.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.  
