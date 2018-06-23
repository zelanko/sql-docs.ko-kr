---
title: Azure Data Lake Store 대상 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSDEST.F1
- SQL11.DTS.DESIGNER.AFPADLSDEST.F1
ms.assetid: d0e86032-2a6b-48b2-898f-e94328474fde
caps.latest.revision: 5
author: yualan
ms.author: yual
manager: jhubbard
ms.openlocfilehash: a68c0299d45a8665d7fb7ad14c92c9a58638c232
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181865"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 대상
  **Azure Data Lake Store 대상** 구성 요소를 사용하면 SSIS 패키지가 Azure Data Lake Store에 데이터를 쓸 수 있습니다. 지원되는 파일 형식은 텍스트, Avro 및 ORC입니다. 
  
## <a name="configure-the-azure-data-lake-store-destination"></a>Azure Data Lake Store 대상 구성 

1. **Azure Data Lake Store 대상** 을 데이터 흐름 디자이너에 끌어서 놓은 다음 두 번 클릭하여 편집기를 표시합니다.  

2.  **Azure Data Lake Store 연결 관리자** 필드에서는 기존 Azure Data Lake Store 연결 관리자를 지정하거나 Azure Data Lake Store 서비스를 참조하는 연결 관리자를 새로 만듭니다.  
  
    1.  **파일 경로** 필드에서는 데이터를 기록할 파일 이름을 지정합니다. 이 파일이 이미 있는 경우 해당 콘텐츠를 덮어쓰게 됩니다.  
  
    2.  **파일 형식** 필드에서는 사용할 파일 형식을 지정합니다.  
  
        파일 형식이 Text이면 **열 구분 기호 문자** 값을 지정해야 합니다. 파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.  

        파일 형식이 ORC이면 해당 플랫폼의 JRE를 설치해야 합니다. 
  
3.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.  