---
title: 온라인 모드로 Analysis Services 데이터베이스에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services, connecting
ms.assetid: 33041234-7106-404f-a289-8e904f32aff2
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4233f9d50cb64bb3827e4dec49251e382ca3c4b3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089662"
---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>온라인 모드로 Analysis Services 데이터베이스에 연결
  기존 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 직접 연결하여 해당 데이터베이스 내의 개체를 직접 수정할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 직접 연결하면 개체 변경이 즉시 수행되며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 내에 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트가 생성되지 않습니다.  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>SQL Server Data Tools를 사용하여 Analysis Services 데이터베이스에 직접 연결하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 엽니다.  
  
2.  **파일** 메뉴에서 **열기** 를 가리킨 다음 **Analysis Services 데이터베이스**를 클릭합니다.  
  
3.  **기존 데이터베이스에 연결**을 선택합니다.  
  
4.  서버 이름과 데이터베이스 이름을 지정합니다.  
  
     데이터베이스 이름을 입력하거나 서버를 쿼리하여 서버의 기존 데이터베이스를 볼 수 있습니다.  
  
5.  **확인**을 클릭합니다.  
  
     이제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 내의 모든 개체를 직접 편집할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 작업 프로젝트 및 데이터베이스 개발 단계](work-with-analysis-services-projects-and-databases-in-development.md)   
 [다차원 모델을 만들 SQL Server Data Tools를 사용 하 여 &#40;SSDT&#41;](creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  