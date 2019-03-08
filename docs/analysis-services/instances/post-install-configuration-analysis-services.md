---
title: 설치 후 구성 (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aadcdb901c39af148b22640413b921aae288f016
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579483"
---
# <a name="post-install-configuration-analysis-services"></a>설치 후 구성(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services를 설치한 후 추가 구성을 수행하여 서버가 완전히 작동하고 일반 용도로 사용 가능하도록 설정해야 합니다. 이 섹션에서는 설치를 완료하는 추가 태스크를 소개합니다. 연결 요구 사항에 따라 인증을 구성해야 할 수도 있습니다( [Analysis Services에 연결](../../analysis-services/instances/connect-to-analysis-services.md)참조).  
  
 이후에 데이터베이스를 배포할 준비가 되면 추가 작업이 필요합니다. 즉, 데이터베이스에서 역할 멤버 자격을 구성하여 데이터 액세스 권한을 사용자에게 부여해야 하며 데이터베이스 백업 및 복구 전략을 디자인하고 데이터를 정기적으로 새로 고칠 수 있도록 예약된 처리 작업이 필요한지 여부를 결정해야 합니다. 데이터베이스 배포 및 관리에 대한 자세한 내용은 다음 링크에서 찾을 수 있습니다. [다차원 Model 데이터베이스](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) 하 고 [테이블 형식 모델 데이터베이스](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)합니다.  
  
## <a name="instance-configuration"></a>인스턴스 구성  
 Analysis Services는 복제 가능한 서비스이므로 단일 서버에 서비스의 인스턴스를 여러 개 설치할 수 있습니다. 각 추가 인스턴스는 SQL Server 설치 프로그램을 사용하여 명명된 인스턴스로 별도로 설치되며 필요한 용도를 지원하도록 독립적으로 구성됩니다. 예를 들어 개발 서버는 비행 레코더를 실행하거나 데이터 스토리지에 대한 기본값을 사용할 수 있습니다. 이러한 기본값은 프로덕션 작업을 지원하는 서버에서 변경될 수도 있습니다. 시스템 구성을 조정해야 하는 또 다른 예는 다른 서비스들이 공유하는 하드웨어에 Analysis Services 인스턴스를 설치하는 경우입니다. 동일한 하드웨어에서 데이터를 많이 사용하는 여러 애플리케이션을 호스팅하는 경우 모든 애플리케이션 간에 사용 가능한 리소스를 최적화하도록 메모리 임계값을 낮추는 서버 속성을 구성해야 할 수 있습니다.  
  
## <a name="post-installation-tasks"></a>설치 후 태스크  
  
|링크|태스크 설명|  
|----------|----------------------|  
|[Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Analysis Services 인스턴스에서 사용하는 TCP 포트를 통해 요청이 라우팅될 수 있도록 Windows 방화벽에서 인바운드 규칙을 만듭니다. 이 태스크는 필수입니다. 인바운드 방화벽 규칙이 정의될 때까지 원격 컴퓨터에서 Analysis Services에 액세스할 수 없습니다.|  
|[Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)|설치 중에 하나 이상의 사용자 계정을 Analysis Services 인스턴스의 관리자 역할에 추가해야 했습니다. 관리 권한은 외부 관계형 데이터베이스에서 제공된 데이터의 처리와 같은 많은 일상적인 서버 작업에 필요합니다. 관리자 역할의 멤버 자격을 추가하거나 수정하려면 이 항목의 정보를 사용하세요.|
|[SQL Server를 실행하는 컴퓨터에서 바이러스 백신 소프트웨어 구성](https://support.microsoft.com/kb/309422) |SQL Server 폴더 및 파일 형식을 제외하도록 바이러스 백신 및 스파이웨어 방지 애플리케이션과 같은 검색 소프트웨어를 구성해야 할 수도 있습니다. Analysis Services에서 사용해야 할 때 검색 소프트웨어가 프로그램이나 데이터 파일을 잠그면 서비스 중단 또는 데이터 손상이 발생할 수 있습니다. |
|[서비스 계정 구성&#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)|설치 중에 Analysis Services 서비스 계정이 프로그램 실행 파일과 데이터베이스 파일에 대한 제어된 액세스를 허용하는 적절한 권한과 함께 프로비전되었습니다. 사후 설치 태스크로, 이제 추가 태스크를 수행할 때 서비스 계정의 사용을 허용할지 여부를 고려해야 합니다. 처리 및 쿼리 작업이 모두 서비스 계정에서 실행될 수 있습니다. 이러한 작업은 서비스 계정에 적절한 권한이 있는 경우에만 성공합니다.|  
|[서버 그룹에 Analysis Services 등록](../../analysis-services/instances/register-an-analysis-services-instance-in-a-server-group.md)|SSMS(SQL Server Management Studio)를 사용하면 SQL Server 인스턴스를 구성하기 위한 서버 그룹을 만들 수 있습니다. 여러 서버 인스턴스로 구성된 확장 가능한 배포는 서버 그룹에서 관리하기가 더 쉽습니다. Analysis Services 인스턴스를 SSMS에서 그룹으로 구성하려면 이 항목의 정보를 사용하세요.|  
|[Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)|설치 중에 서버에서 실행되는 모델의 유형(다차원 또는 테이블 형식)을 결정하는 서버 모드를 선택했습니다. 서버 모드를 잘 모르는 경우 이 항목의 정보를 사용하여 설치된 모드를 확인하세요.|  
|[Analysis Services 인스턴스 이름 바꾸기](../../analysis-services/instances/rename-an-analysis-services-instance.md)|설명이 포함된 이름은 서버 모드가 서로 다른 여러 인스턴스나 조직의 부서나 팀에서 주로 사용하는 인스턴스를 구별하는 데 도움이 될 수 있습니다. 인스턴스 이름을 설치의 효율적인 관리에 도움이 되는 이름으로 변경하려면 이 항목의 정보를 사용하여 방법을 알아보세요.|  
  
## <a name="next-steps"></a>다음 단계  
 클라이언트 라이브러리를 사용하여 Microsoft 애플리케이션 또는 사용자 지정 애플리케이션에서 Analysis Services에 연결하는 방법을 알아봅니다. 솔루션 요구 사항에 따라 Kerberos 인증에 대해 서비스를 구성해야 할 수도 있습니다. 도메인 경계를 넘어야 하는 연결에는 HTTP 액세스가 필요합니다. 다음 단계에 대한 지침은 [Connect to Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md) 을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2016 설치](../../database-engine/install-windows/installation-for-sql-server-2016.md)   
 [다차원 및 데이터 마이닝 모드에서 Analysis Services 설치](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Analysis Services 설치](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [파워 피벗 모드에서 Analysis Services 설치](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
