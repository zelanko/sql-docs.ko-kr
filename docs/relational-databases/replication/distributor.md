---
title: 배포자 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replicationutilities.selectdistributor.f1
ms.assetid: 787f0e9c-09dd-438a-bc04-5b8f99c127b8
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 664ceea195e327b9c301ed1206eba014c8adf2a8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287884"
---
# <a name="distributor"></a>배포자
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **배포자** 페이지는 배포 구성 마법사 및 새 게시 마법사에 표시됩니다. 배포자는 배포 데이터베이스를 포함하고 모든 유형의 복제에 대한 메타데이터 및 기록 데이터를 저장하는 서버입니다. 또한 배포자는 트랜잭션 복제에 대한 트랜잭션을 저장합니다. 배포자는 게시자와 별개인 서버(원격 배포자)가 되거나 게시자와 같은 서버(로컬 배포자)가 될 수 있습니다. 배포자의 역할은 구현하는 복제의 유형에 따라 달라집니다. 일반적으로 배포자의 역할은 병합 복제 및 스냅샷 복제보다 트랜잭션 복제에서 훨씬 큽니다. 보통 병합 및 스냅샷 복제에서는 로컬 배포자를 사용하지만 사용률이 매우 높은 시스템에서는 트랜잭션 배포에서 원격 배포자를 사용하는 것이 유리할 수 있습니다.  
  
 배포자가 있는 서버에는 다음과 같은 추가 리소스가 필요합니다.  
  
-   게시에 대한 스냅샷 파일이 저장되어 있는 경우(일반적으로 배포자에 저장되어 있음) 추가 디스크 공간  
  
-   배포 데이터베이스를 저장할 추가 디스크 공간  
  
-   배포자에서 실행되는 밀어넣기 구독에 대해 복제 에이전트가 사용할 추가 프로세서  
  
 배포자로 선택된 서버는 복제 및 해당 서버의 다른 작업을 지원하기 위해 충분한 디스크 공간과 처리 성능이 있어야 합니다.  
  
## <a name="options"></a>옵션  
 **'\<ServerName>'을 자체 배포자로 사용합니다. SQL Server에서 배포 데이터베이스와 로그를 만듭니다.**  
 연결된 서버를 배포자로 구성하려면 이 옵션을 선택합니다.  
  
 **다음 서버를 배포자로 사용(참고: 선택한 서버는 이미 배포자로 구성되어 있어야 함)**  
 다른 서버를 배포자로 구성하려면 이 옵션을 선택하고 서버 이름을 클릭합니다.  
  
 **추가**  
 배포자로 사용할 서버가 목록에 없으면 **추가** 를 클릭하여 서버를 식별하고 목록에 추가합니다.  
  
> [!NOTE]  
>  원격 서버를 배포자로 사용하려면 원격 서버가 이미 배포자로 구성되어 있어야 합니다. 이 마법사가 실행 중인 서버는 해당 배포자에서 게시자로 설정되어 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
