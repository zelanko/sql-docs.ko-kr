---
title: 배포 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributiondatabase.f1
ms.assetid: 5b42a083-7a11-41d8-9e3f-320c7c907237
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 283fd67d14d57c3d1d5d60dd9d8de2a159ca6d5e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721368"
---
# <a name="distribution-database"></a>배포 데이터베이스
  배포 데이터베이스는 모든 유형의 복제에 대한 메타데이터 및 기록 데이터와 트랜잭션 복제에 대한 트랜잭션을 저장합니다.  
  
 대부분의 경우 배포 데이터베이스는 하나면 충분합니다. 그러나 여러 게시자가 단일 배포자를 사용하는 경우에는 각 게시자에 대해 배포 데이터베이스를 만들어 보십시오. 이렇게 하면 각 배포 데이터베이스를 통한 데이터 흐름이 고유하게 유지됩니다. 배포 구성 마법사를 사용하여 배포자에 대한 배포 데이터베이스를 하나 지정할 수 있습니다. 필요한 경우 **배포자 속성** 대화 상자에서 추가 배포 데이터베이스를 지정하십시오.  
  
## <a name="options"></a>옵션  
 **배포 데이터베이스 이름**  
 배포 데이터베이스 이름을 입력합니다. 배포 데이터베이스의 기본 이름은 'distribution'입니다. 이름을 지정하는 경우 이름은 최대 128자가 될 수 있으며, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유해야 하고, 식별자 규칙을 따라야 합니다. 자세한 내용은 [Database Identifiers](../databases/database-identifiers.md)을 참조하세요.  
  
 **배포 데이터베이스 파일 폴더** 및 **배포 데이터베이스 로그 파일 폴더**  
 배포 데이터베이스 및 로그 파일에 대한 경로를 입력합니다. 경로는 배포자에 로컬인 디스크여야 하므로 로컬 드라이브 문자와 콜론(예: C:)으로 시작해야 합니다. 매핑된 드라이브 문자와 네트워크 경로는 유효하지 않습니다.  
  
> [!NOTE]  
>  배포 데이터베이스 로그를 배포 데이터베이스에서 별개의 디스크 드라이브에 두어 트랜잭션을 기록하는 데 걸리는 시간을 줄이고 복제 성능을 향상시킬 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](configure-distribution.md)   
 [게시 및 배포 구성](configure-publishing-and-distribution.md)   
 [배포자 및 게시자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)  
  
  
