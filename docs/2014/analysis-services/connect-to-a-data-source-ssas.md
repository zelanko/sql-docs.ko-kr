---
title: 데이터 원본 (SSAS)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.conndatasource.f1
ms.assetid: 1e2b17e9-092b-4af1-8a58-c52b8fe10ff1
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f33af08d91f2c8e739c9295daed0ae47563ede51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090567"
---
# <a name="connect-to-a-data-source-ssas"></a>데이터 원본에 연결(SSAS)
  **테이블 가져오기 마법사** 의 이 페이지에서는 관계형 데이터베이스, 데이터 피드, 파일 등과 같은 다양한 데이터 원본을 대상으로 새 데이터 원본 연결을 만들 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 마법사에 액세스하려면 **모델** 메뉴에서 **데이터 원본에서 가져오기**를 클릭합니다.  
  
 데이터 원본에 연결하려면 컴퓨터에 적절한 공급자가 설치되어 있어야 합니다. 작업 영역 데이터베이스 서버에도 적절한 공급자가 설치되어 있어야 합니다. 32비트(x86) 서버의 경우 32비트 공급자가 설치되어 있어야 하며 64비트(x64) 서버의 경우 64비트 공급자가 설치되어 있어야 합니다.  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 항상 아키텍처에 관계 없이 32 비트 프로세스에서 실행 됩니다. 64비트 컴퓨터에서 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 를 실행하는 경우 데이터 공급자를 설치할 때 다음 사항에 주의해야 합니다.  
  
-   32비트와 64비트 공급자를 함께 설치할 수 있는 공급자의 경우 두 공급자를 모두 설치해야 합니다.  
  
-   ACE 공급자의 경우 64비트 버전의 공급자를 설치해야 합니다. Office에서는 ACE 공급자가 자동으로 설치되므로 작업 영역 데이터베이스 서버를 호스팅하는 64비트 컴퓨터에서 32비트 버전의 Microsoft Office를 실행해서는 안 됩니다.  
  
     ACE 공급자는 텍스트, Excel 및 Access 파일에서 가져오기 작업을 수행하는 데 사용됩니다. 이러한 데이터 원본에 대한 지원이 필요하지 않은 경우 64비트 작업 영역 데이터베이스 서버를 실행하는 컴퓨터에서 32비트 버전의 Microsoft Office를 실행할 수 있습니다.  
  
-   32비트와 64비트 공급자를 함께 설치할 수 없는 기타 공급자의 경우에는 32비트 공급자를 설치해야 합니다. 64비트 컴퓨터만 사용할 수 있는 경우 64비트 공급자가 설치된 원격 컴퓨터를 작업 영역 데이터베이스 서버로 사용해야 합니다.  
  
  