---
title: 온라인 모드로 Analysis Services 데이터베이스에 연결 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 612e538ef01040778497242606115a01c6ef6921
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>온라인 모드로 Analysis Services 데이터베이스에 연결
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  기존 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 직접 연결하여 해당 데이터베이스 내의 개체를 직접 수정할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 직접 연결하면 개체 변경이 즉시 수행되며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 내에 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트가 생성되지 않습니다.  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>SQL Server Data Tools를 사용하여 Analysis Services 데이터베이스에 직접 연결하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 엽니다.  
  
2.  **파일** 메뉴에서 **열기** 를 가리킨 다음 **Analysis Services 데이터베이스**를 클릭합니다.  
  
3.  **기존 데이터베이스에 연결**을 선택합니다.  
  
4.  서버 이름과 데이터베이스 이름을 지정합니다.  
  
     데이터베이스 이름을 입력하거나 서버를 쿼리하여 서버의 기존 데이터베이스를 볼 수 있습니다.  
  
5.  **확인**을 클릭합니다.  
  
     이제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 내의 모든 개체를 직접 편집할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 작업 프로젝트 및 데이터베이스 개발 단계](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md)   
 [SQL Server 데이터 도구 & #40;를 사용 하 여 다차원 모델 만들기 SSDT & #41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  
