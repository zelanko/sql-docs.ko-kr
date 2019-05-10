---
title: 다국어 및 글로벌 배포(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c3d485f8-867c-4aa2-a90d-f38fda192534
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d53ff45452f90c5cf29f376ba01a395d2bbccf65
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482960"
---
# <a name="multi-lingual-and-global-deployments-master-data-services"></a>다국어 및 글로벌 배포(Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 모든 언어 구성 요소 및 도구 배포를 지원합니다. 자세한 내용은 [Local Language Versions in SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md)을 참조하세요.  
  
## <a name="how-languages-are-used"></a>언어 사용 방식  
 다음 표에서는 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 구성 요소 및 도구의 언어 지원에 대해 설명합니다.  
  
|구성 요소 또는 도구|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 설치 프로그램|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 응용 프로그램이 설치 언어와 다른 언어로 사용 및 지원되도록 하려면 영어 설치 프로그램을 선택합니다. 자세한 내용은 아래의 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 설명을 참조하십시오.|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 언어는 설치 언어에 따라 결정됩니다. 예를 들어 설치 언어로 독일어를 선택한 경우 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 는 해당 컴퓨터에서 독일어로 사용할 수 있습니다.|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|설치 프로그램을 영어로 실행하면 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 웹 애플리케이션을 모든 애플리케이션 언어로 사용할 수 있으며 모든 애플리케이션 언어가 지원됩니다. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 에는 이러한 응용 프로그램 언어가 표시되며 클라이언트 웹 브라우저의 언어 기본 설정에 따라 로캘별 입력이 적용됩니다. 언어 기본 설정이 지원되지 않는 애플리케이션 언어로 구성된 경우 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 는 기본적으로 영어로 지정됩니다.<br /><br /> 영어가 아닌 다른 언어로 설치 프로그램을 실행하면 기타 모든 애플리케이션 언어에 대한 리소스가 포함되지만 클라이언트에서 선택한 설치 언어 이외의 언어로 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 를 사용할 수 있는 시나리오가 지원되지 않습니다. 설치 언어와 다른 언어의 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 에 액세스하려고 하면 애플리케이션의 데이터 표시 및 입력에 문제가 발생할 수 있습니다.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 데이터베이스의 정보는 어떠한 로캘에도 특정하지 않습니다. 따라서 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 에서는 클라이언트 웹 브라우저의 언어 기본 설정에 따른 형식으로 날짜 및 숫자와 같은 정보를 표시하는 방법을 결정합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [MDS(Master Data Services) 설치](install-master-data-services.md)  
  
  
