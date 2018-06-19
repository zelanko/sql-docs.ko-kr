---
title: Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 10/12/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9c6b996c-e768-4bf5-837f-5436ed9cea1d
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc67b62db9a058511bafed2447a0f9e256337fca
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35310552"
---
# <a name="data-quality-services"></a>데이터베이스 엔진 서비스

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssDQSnoversionLong](../includes/ssdqsnoversionlong-md.md)](DQS)는 지식 기반 데이터 품질 제품입니다. DQS를 사용하면 기술 자료를 작성한 다음 해당 기술 자료를 사용하여 데이터 수정, 강화, 표준화 및 중복 제거를 포함한 다양한 핵심 데이터 품질 태스크를 수행할 수 있습니다. DQS를 통해 참조 데이터 공급자가 제공하는 클라우드 기반 참조 데이터 서비스를 사용하여 데이터 정리를 수행할 수 있습니다. DQS는 또한 데이터 품질 태스크에 통합된 프로파일링을 제공하여 데이터의 무결성을 분석할 수 있게 해줍니다.  
  
 DQS는 모두 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 의 일부로 설치되는 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]및 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 구성됩니다. [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]는 데이터 품질 기능 및 저장소가 포함된 세 가지 SQL Server 카탈로그로 구성되는 SQL Server 인스턴스 기능입니다. [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]는 비즈니스 사용자, 정보 근로자 및 IT 전문가가 컴퓨터 기반 데이터 품질 분석을 수행하고 해당 데이터 품질을 대화형으로 관리하기 위해 사용할 수 있는 SQL Server 공유 기능입니다. 또한 모두 DQS를 기반으로 하는 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] 및 MDS(Master Data Services) 데이터 품질 기능을 사용하여 데이터 품질 프로세스를 수행할 수 있습니다.  
  
 DQS 설치에 대한 자세한 내용은 [Install Data Quality Services](../data-quality-services/install-windows/install-data-quality-services.md)를 참조하십시오. 기존 버전의 DQS를 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]로 업그레이드하려면 [Data Quality Services 업그레이드](../database-engine/install-windows/upgrade-data-quality-services.md)를 참조하세요.  
  
 **영역별 내용 찾아보기**  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [Data Quality Client 응용프로그램](../data-quality-services/data-quality-client-application.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [DQS 기술 자료 및 도메인](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [데이터 품질 프로젝트](../data-quality-services/data-quality-projects-dqs.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [데이터 정리](../data-quality-services/data-cleansing.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [데이터 일치](../data-quality-services/data-matching.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [DQS의 참조 데이터 서비스](../data-quality-services/reference-data-services-in-dqs.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [DQS의 데이터 프로파일링 및 알림](../data-quality-services/data-profiling-and-notifications-in-dqs.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [DQS 관리](../data-quality-services/dqs-administration.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [DQS 보안](../data-quality-services/dqs-security.md)  
  
## <a name="see-also"></a>참고 항목  
 [Data Quality Services 소개](../data-quality-services/introduction-to-data-quality-services.md)   
 [Data Quality Services 개념](../data-quality-services/data-quality-services-concepts.md)   
 [DQS 리소스](http://technet.microsoft.com/sqlserver/hh780961)   
 [SQL Server 리소스 센터](http://go.microsoft.com/fwlink/?linkID=219676)  
  
  
