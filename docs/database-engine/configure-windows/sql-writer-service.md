---
title: SQL 기록기 서비스 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- VDI [SQL Server]
- restoring [SQL Server], SQL Writer Service
- backups [SQL Server], while SQL Server running
- Volume Shadow Copy Service
- volume backups while running [SQL Server]
- Virtual Backup Device Interface [SQL Server]
- SQL Writer Service
- services [SQL Server], SQL Writer
- MSDE Writer
- VSS
ms.assetid: 0f299867-f499-4c2a-ad6f-b2ef1869381d
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b6fab60401596743dc1cc38dd0c115e42ec89c71
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32865568"
---
# <a name="sql-writer-service"></a>SQL 기록기 서비스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL 기록기 서비스는 볼륨 섀도 복사본 서비스 프레임워크를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 백업 및 복원을 위한 추가 기능을 제공합니다.  
  
 SQL 기록기 서비스는 자동으로 설치되며 VSS(볼륨 섀도 복사본 서비스) 응용 프로그램이 백업 또는 복원을 요청할 때 실행되어야 합니다. 서비스를 구성하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 서비스 애플릿을 사용합니다. SQL 기록기 서비스는 모든 운영 체제에 설치됩니다.  
  
## <a name="purpose"></a>용도  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 실행 중에 데이터 파일을 잠그고 이 파일에 독점적으로 액세스합니다. SQL 기록기 서비스가 실행 중이 아니면 Windows에서 실행 중인 백업 프로그램이 데이터 파일에 액세스할 수 없으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 사용하여 백업을 수행해야 합니다.  
  
 SQL 기록기 서비스를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 동안에도 Windows 백업 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일을 복사할 수 있습니다.  
  
## <a name="volume-shadow-copy-service"></a>볼륨 섀도 복사본 서비스  
 VSS는 시스템의 응용 프로그램이 볼륨에 계속 쓰는 동안 볼륨 백업을 수행할 수 있도록 프레임워크를 구현하는 COM API 집합입니다. VSS는 디스크의 데이터를 업데이트하는 사용자 응용 프로그램(기록자)과 응용 프로그램을 백업하는 사용자 응용 프로그램(요청자) 간 조정을 허용하는 일관된 인터페이스를 제공합니다.  
  
 VSS는 제공하는 서비스의 성능과 안정성을 저하시키지 않고도 실행 중인 시스템, 특히 서버에서 안정적인 백업용 이미지를 캡처하고 복사합니다. VSS에 대한 자세한 내용은 Windows 설명서를 참조하십시오.  
  
## <a name="virtual-backup-device-interface-vdi"></a>VDI(Virtual Backup Device Interface)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 독립 소프트웨어 공급업체들이 백업 및 복원 작업을 지원하기 위해 해당 제품에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 통합할 수 있도록 하는 VDI(Virtual Backup Device Interface)라는 API를 제공합니다. 이러한 API는 최고의 안정성과 성능을 제공하도록 설계되었으며 모든 최신 기능과 스냅숏 백업 기능을 비롯하여 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원 기능을 지원합니다.  
  
## <a name="permissions"></a>사용 권한  
 SQL 기록기 서비스는 **로컬 시스템** 계정으로 실행해야 합니다. SQL 기록기 서비스는 **NT Service\SQLWriter** 로그인을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결합니다. **NT Service\SQLWriter** 로그인을 사용하면 SQL 기록기 프로세스가 **로그인 없음**으로 지정된 계정에서 보다 낮은 권한 수준으로 실행될 수 있으므로 취약성이 제한됩니다. SQL 기록기 서비스를 사용하지 않도록 설정하면 System Center Data Protection Manager와 같이 VSS 스냅숏에 의존하는 모든 유틸리티와 일부 타사 제품이 손상되거나 저하되며 일관성이 없는 데이터베이스 백업을 수행할 위험이 있습니다. SQL 기록기 서비스가 실행되는 시스템인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](과)와 호스트 시스템(가상 머신의 경우)에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 백업을 제외한 어떤 것도 사용할 필요가 없는 경우 SQL 기록기 서비스를 사용하지 않도록 설정해도 괜찮으며 로그인을 제거해도 됩니다.  SQL 기록기 서비스는 시스템 또는 볼륨 수준 백업에서 호출될 수 있습니다. 이때 백업이 직접 스냅숏을 기반으로 하는지 여부는 관계가 없습니다. 일부 시스템 백업 제품은 VSS를 사용하여 열려 있거나 잠긴 파일에 의해 차단되는 것을 방지합니다. SQL 기록기 서비스는 작업 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 모든 I/O를 잠깐 중지시키기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 승격된 권한을 필요로 합니다.  
  
## <a name="features"></a>기능  
 SQL 기록기에서 지원하는 기능  
  
-   전체 텍스트 카탈로그를 포함한 전체 데이터베이스 백업 및 복원  
  
-   차등 백업 및 복원  
  
-   복원(이동)  
  
-   데이터베이스 이름 바꾸기  
  
-   복사 전용 백업  
  
-   데이터베이스 스냅숏 자동 복구  
  
 SQL 기록기에서 지원하지 않는 기능  
  
-   로그 백업  
  
-   파일 및 파일 그룹 백업  
  
-   페이지 복원  
  
  
