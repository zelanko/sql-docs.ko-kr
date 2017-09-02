---
title: "설치 마법사 도움말 | Microsoft Docs"
ms.custom: 
ms.date: 2017-04-21
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
caps.latest.revision: 62
ms.author: mikeray
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: HT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 4b16feb70ed6de54240e3335a42ce6df8fa57b81
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="installation-wizard-help"></a>설치 마법사 도움말

이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 일부 구성 페이지에 대해 설명합니다. 

## <a name="instance-configuration"></a>인스턴스 구성
**설치 마법사의** 인스턴스 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 만들지 또는 명명된 인스턴스를 만들지 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 아직 설치되지 않은 경우 명명된 인스턴스를 지정하지 않으면 기본 인스턴스가 만들어집니다.  
  
각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 특정 데이터 정렬과 기타 옵션이 지정된 고유의 서비스 집합으로 구성됩니다. 디렉터리 구조, 레지스트리 구조 및 서비스 이름은 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중 작성한 인스턴스 이름과 특정 인스턴스 ID를 반영합니다.  
  
 인스턴스는 기본 인스턴스이거나 명명된 인스턴스입니다. 기본 인스턴스 이름은 MSSQLSERVER입니다. 연결을 위해 클라이언트에서 인스턴스 이름을 지정할 필요는 없습니다. 명명된 인스턴스는 설치 중 사용자가 결정합니다. 기본 인스턴스를 먼저 설치하지 않고도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 명명된 인스턴스로 설치할 수 있습니다. 버전과 관계없이 한 번에 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치만 기본 인스턴스가 될 수 있습니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용할 경우 **인스턴스 구성** 페이지에서 준비 인스턴스를 완료할 때 인스턴스 이름을 지정할 수 있습니다. 시스템에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기존 기본 인스턴스가 없는 경우 완료하려는 준비 인스턴스를 기본 인스턴스로 구성하도록 선택할 수 있습니다.  
  
### <a name="multiple-instances"></a>여러 인스턴스  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 단일 서버 또는 프로세서에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지원하지만 하나의 인스턴스만 기본 인스턴스가 될 수 있습니다. 다른 모든 인스턴스는 명명된 인스턴스여야 합니다. 한 컴퓨터에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 동시에 실행할 수 있으며 각 인스턴스는 다른 인스턴스와 독립적으로 실행됩니다.  
  
 자세한 내용은 [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md)을 참조하세요.  
  
### <a name="options"></a>옵션  
 장애 조치(Failover) 클러스터 인스턴스만 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 클러스터 네트워크 이름을 지정합니다. 이 이름은 네트워크에서 장애 조치(Failover) 클러스터 인스턴스를 식별합니다.  
  
 기본 또는 명명된 인스턴스 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스와 명명된 인스턴스 중 설치할 항목을 결정할 때 다음 정보를 고려하십시오.  
  
-   데이터베이스 서버에 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치할 경우 이 인스턴스는 기본 인스턴스여야 합니다.  
  
-   동일한 컴퓨터에 여러 인스턴스를 설치할 경우에는 명명된 인스턴스를 사용합니다. 한 서버에서 기본 인스턴스 한 개만 호스팅할 수 있습니다.  
  
-   [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 를 설치하는 응용 프로그램은 이를 명명된 인스턴스로 설치해야 합니다. 이렇게 하면 여러 응용 프로그램을 동일한 컴퓨터에 설치한 경우 충돌을 최소화할 수 있습니다.  
  
 **기본 인스턴스**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 설치하려면 이 옵션을 선택합니다. 한 컴퓨터에서는 기본 인스턴스를 하나만 호스팅할 수 있으며 나머지 인스턴스는 모두 명명된 인스턴스여야 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 인스턴스가 설치되어 있으면 동일한 컴퓨터에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 인스턴스를 추가할 수 있습니다.  
  
 **명명된 인스턴스**  
 새 명명된 인스턴스를 만들려는 경우 이 옵션을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름을 지정할 때 다음에 주의합니다.  
  
-   인스턴스 이름은 대/소문자를 구분하지 않습니다.  
  
-   인스턴스 이름은 밑줄(_)로 시작하거나 끝낼 수 없습니다.  
  
-   인스턴스 이름에는 용어 "Default" 또는 다른 예약 키워드를 사용할 수 없습니다. 인스턴스 이름에 예약 키워드를 사용한 경우 설치 오류가 발생합니다. 자세한 내용은 [예약된 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)를 참조하세요.  
  
-   인스턴스 이름으로 MSSQLServer를 지정하면 기본 인스턴스가 만들어집니다.  
  
-   [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 는 항상 '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]'이라고 명명된 인스턴스로 설치됩니다. 이 기능 역할에는 다른 인스턴스 이름을 지정할 수 없습니다.  
  
-   인스턴스 이름은 16자로 제한됩니다.  
  
-   인스턴스 이름의 첫 글자는 문자여야 합니다. 허용되는 문자는 유니코드 표준 2.0에서 정의된 문자입니다. 여기에는 a - z, A - Z의 라틴어 문자와 기타 언어의 문자가 포함됩니다.  
  
-   이어지는 글자는 유니코드 표준 2.0에 정의된 문자, 기본 라틴어 또는 기타 국가별 스크립트에 정의된 숫자, 달러 기호($) 또는 밑줄(_)이 될 수 있습니다.  
  
-   공백이나 다른 특수 문자는 인스턴스 이름에 사용할 수 없습니다. 백슬래시(\\), 쉼표(,), 콜론(:), 세미콜론(;), 작은따옴표('), 앰퍼샌드(&), 하이픈(-) 및 @ 기호도 사용할 수 없습니다.  
  
     현재 Windows 코드 페이지에서 유효한 문자만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름에 사용할 수 있습니다. 지원되지 않는 유니코드 문자를 사용할 경우 설치 오류가 발생합니다.  
  
 **감지된 인스턴스 및 기능**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 실행 중인 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 구성 요소 목록을 확인합니다.  
  
 **인스턴스 ID** - 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 이는 기본 인스턴스와 명명된 인스턴스에 모두 해당됩니다. 기본 인스턴스의 경우 인스턴스 이름 및 인스턴스 ID는 MSSQLSERVER입니다. 기본 인스턴스 ID가 아닌 ID를 사용하려면 **인스턴스 ID** 필드에 해당 ID를 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용할 경우 이 페이지에 표시되는 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 프로세스의 이미지 준비 단계 중에 지정한 인스턴스 ID입니다. 이미지 완료 단계에서는 다른 인스턴스 ID를 지정할 수 없습니다.  
  
> [!NOTE]  
>  밑줄(_)로 시작되거나 숫자 기호(#) 또는 달러 기호($)가 들어 있는 인스턴스 ID는 지원되지 않습니다.  
  
 디렉터리, 파일 위치 및 인스턴스 ID 명명에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.  
  
 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 구성 요소는 하나의 단위로 관리됩니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩 및 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 구성 요소에 적용됩니다.  
  
 같은 인스턴스 이름을 공유하는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 다음 조건을 충족해야 합니다.  
  
-   **같은 버전**  
  
-   **같은 에디션**  
  
-   **같은 언어 설정**  
  
-   **같은 클러스터형 상태**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 클러스터 인식형이 아닙니다.  
  
-   **같은 운영 체제**  
  
## <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services 구성 - 계정 프로비전
  이 페이지를 사용하여 서버 모드를 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 제한 없이 액세스해야 하는 사용자나 서비스에 관리 권한을 부여할 수 있습니다. 설치 마법사에서는 로컬 Windows Group BUILTIN\Administrators를 설치할 인스턴스의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 관리자 역할에 자동으로 추가하지 않습니다. 로컬 Administrators 그룹을 서버 관리자 역할에 추가하려면 해당 그룹을 명시적으로 지정해야 합니다.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 시에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 팜에서 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 서버 배포를 담당하는 SharePoint 팜 관리자 또는 서비스 관리자에게 관리 권한을 부여해야 합니다.  
  
### <a name="options"></a>옵션  
 **서버 모드** - 서버 모드는 서버에 배포할 수 있는 Analysis Services 데이터베이스의 유형을 지정합니다. 서버 모드는 설치 중에 결정되며 나중에 수정할 수 없습니다. 각 모드는 함께 사용할 수 없습니다. 즉, 기존의 OLAP 및 테이블 형식 모델 솔루션을 모두 지원하려면 각각 서로 다른 모드에 맞게 구성된 두 개의 Analysis Services 인스턴스가 필요합니다.  
  
 **관리자 지정** - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 서버 관리자를 한 명 이상 지정해야 합니다. 지정한 사용자 또는 그룹은 설치할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 서버 관리자 역할 멤버가 됩니다. 이러한 사용자 또는 그룹은 소프트웨어를 설치할 컴퓨터와 동일한 도메인의 Windows 도메인 사용자 계정이어야 합니다.  
  
> [!NOTE]  
>  UAC(사용자 계정 컨트롤)는 관리 동작이나 응용 프로그램을 실행하려면 관리자가 승인을 해야 하는 Windows 보안 기능입니다. UAC는 기본적으로 설정되므로, 높은 권한을 필요로 하는 특정 작업을 허용하라는 메시지가 표시됩니다. UAC를 구성하여 기본 동작을 변경하거나 특정 프로그램에 대해 UAC를 사용자 지정할 수 있습니다. UAC 및 UAC 구성에 대한 자세한 내용은 [사용자 계정 컨트롤 단계별 가이드](http://go.microsoft.com/fwlink/?linkid=196350) 및 [사용자 계정 컨트롤(Wikipedia)0](http://go.microsoft.com/fwlink/?linkid=196351)을 참조하세요.  
  
### <a name="see-also"></a>관련 항목:  
 [서비스 계정 구성&#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md) [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

 ## <a name="analysis-services-configuration---data-directories"></a>Analysis Services 구성 - 데이터 디렉터리
  다음 표의 기본 디렉터리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있습니다. 이러한 파일에 대한 액세스 권한은 설치 중에 만들어져 프로비전되는 SQLServerMSASUser$\<instance> 보안 그룹의 멤버와 로컬 관리자에게 부여됩니다.  
  
### <a name="uielement-list"></a>UIElement 목록  
  
|설명|기본 디렉터리|권장 사항|  
|-----------------|-----------------------|---------------------|  
|데이터 루트 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data\ |\Program files\Microsoft SQL Server\ 폴더가 제한된 권한으로 보호되어 있는지 확인하십시오. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 성능은 대부분의 구성에서 데이터 디렉터리가 있는 저장소의 성능에 따라 달라집니다. 이 디렉터리는 시스템에 연결된 성능이 가장 높은 저장소에 두십시오. 장애 조치(Failover) 클러스터 설치의 경우 공유 디스크에 데이터 디렉터리를 만들어야 합니다.|  
|로그 파일 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log\ |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그 파일 디렉터리이며 FlightRecorder 로그를 포함합니다. 비행 레코더 기간을 늘려야 하는 경우 로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|임시 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp\ |Temp 디렉터리도 성능이 뛰어난 저장소 하위 시스템에 두십시오.|  
|백업 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup\ |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 백업 파일의 디렉터리입니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 시에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 파일도 캐시합니다.<br /><br /> 데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스를 위한 사용자 그룹에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
### <a name="notes"></a>참고  
  
-   SharePoint 팜에 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 응용 프로그램 파일, 데이터 파일 및 속성을 콘텐츠 데이터베이스와 서비스 응용 프로그램 데이터베이스에 저장합니다.  
  
-   기존 설치에 기능을 추가할 경우 이전에 설치한 기능의 위치를 변경하거나 새 기능의 위치를 지정할 수 없습니다.  

-   SQL Server 폴더 및 파일 형식을 제외하도록 바이러스 백신 및 스파이웨어 방지 응용 프로그램과 같은 검색 소프트웨어를 구성해야 할 수도 있습니다. 자세한 내용은 [SQL Server를 실행하는 컴퓨터에서 바이러스 백신 소프트웨어](https://support.microsoft.com/kb/309422) 지원 문서를 검토하세요.
  
-   기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소도 별도의 디렉터리에 설치해야 합니다.  
  
-   다음과 같은 위치에는 프로그램 파일 및 데이터 파일을 설치할 수 없습니다.  
  
    -   이동식 디스크 드라이브  
  
    -   압축 파일 시스템  
  
    -   시스템 파일이 있는 디렉터리  
  
### <a name="see-also"></a>관련 항목:  
 디렉터리, 파일 위치 및 인스턴스 ID 명명에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.  
  
## <a name="database-engine-configuration---data-directories"></a>데이터베이스 엔진 구성 - 데이터 디렉터리
  이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로그램 및 데이터 파일의 설치 위치를 지정할 수 있습니다. 설치 유형에 따라 지원되는 저장소에 로컬 디스크, 공유 저장소 또는 SMB 파일 서버가 포함될 수 있습니다.  
  
 SMB 파일 공유를 디렉터리로 지정하려면 지원되는 UNC 경로를 수동으로 입력해야 합니다. SMB 파일 공유를 찾아볼 수는 없습니다. SMB 파일 공유에 지원되는 UNC 경로 형식은 \\\Servername\ShareName\\....입니다.  
  
### <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에 대한 지원되는 저장소 유형 및 기본 디렉터리를 보여 줍니다.  
  
### <a name="uielement-list"></a>UIElement 목록  
  
|설명|지원되는 저장소 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|데이터 루트 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.|  
|사용자 데이터베이스 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data |사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.|  
|사용자 데이터베이스 로그 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|백업 디렉터리|로컬 디스크, SMB 파일 서버, 공유 저장소*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup|데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 위한 사용자 계정에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
 *공유 디스크가 지원되기는 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에는 사용하지 않는 것이 좋습니다.  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스에 대한 지원되는 저장소 유형 및 기본 디렉터리를 보여 줍니다.  
  
|설명|지원되는 저장소 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|데이터 루트 디렉터리|공유 저장소, SMB 파일 서버|\<드라이브:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> 팁: **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.|  
|사용자 데이터베이스 디렉터리|공유 저장소, SMB 파일 서버|\<드라이브:>Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> 팁: **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.|  
|사용자 데이터베이스 로그 디렉터리|공유 저장소, SMB 파일 서버|\<드라이브:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> 팁: **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|백업 디렉터리|로컬 디스크, 공유 저장소, SMB 파일 서버|\<드라이브:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup<br /><br /> 팁: **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 SQL Server 서비스를 위한 사용자 계정에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
### <a name="security-considerations"></a>보안 고려 사항  
 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.  
  
 SMB 파일 서버에는 다음과 같은 권장 사항이 적용됩니다.  
  
-   SMB 파일 서버가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정은 도메인 계정이어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정은 데이터 디렉터리로 사용되는 SMB 파일 공유 폴더에 대해 FULL CONTROL NTFS 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정에는 SMB 파일 서버에 대한 SeSecurityPrivilege 권한이 부여되어야 합니다. 이 권한을 부여하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 계정을 **감사 및 보안 로그 관리** 정책에 추가합니다. 이 설정은 **로컬 보안 정책** 콘솔의 **로컬 정책** 에 있는 **사용자 권한 지정** 섹션에서 사용할 수 있습니다.  
  
### <a name="notes"></a>참고  
  
-   기존 설치에 기능을 추가할 경우 이전에 설치한 기능의 위치를 변경할 수 없으며 새 기능의 위치를 지정할 수도 없습니다.  
  
-   기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소도 별도의 디렉터리에 설치해야 합니다.  
  
-   다음과 같은 위치에는 프로그램 파일 및 데이터 파일을 설치할 수 없습니다.  
  
    -   이동식 디스크 드라이브  
  
    -   압축 파일 시스템  
  
    -   시스템 파일이 있는 디렉터리  
  
    -   장애 조치(failover) 클러스터 인스턴스의 매핑된 네트워크 드라이브  
  
### <a name="see-also"></a>관련 항목:  
### <a name="analysis-services-configuration---data-directories"></a>Analysis Services 구성 - 데이터 디렉터리
  다음 표의 기본 디렉터리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있습니다. 이러한 파일에 대한 액세스 권한은 설치 중에 만들어져 프로비전되는 SQLServerMSASUser$\<instance> 보안 그룹의 멤버와 로컬 관리자에게 부여됩니다.  
  
#### <a name="uielement-list"></a>UIElement 목록  
  
|설명|기본 디렉터리|권장 사항|  
|-----------------|-----------------------|---------------------|  
|데이터 루트 디렉터리 |C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data |\Program files\Microsoft SQL Server\ 폴더가 제한된 권한으로 보호되어 있는지 확인하십시오. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 성능은 대부분의 구성에서 데이터 디렉터리가 있는 저장소의 성능에 따라 달라집니다. 이 디렉터리는 시스템에 연결된 성능이 가장 높은 저장소에 두십시오. 장애 조치(Failover) 클러스터 설치의 경우 공유 디스크에 데이터 디렉터리를 만들어야 합니다.|  
|로그 파일 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그 파일 디렉터리이며 FlightRecorder 로그를 포함합니다. 비행 레코더 기간을 늘려야 하는 경우 로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|임시 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp |Temp 디렉터리도 성능이 뛰어난 저장소 하위 시스템에 두십시오.|  
|백업 디렉터리|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 백업 파일의 디렉터리입니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 시에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 파일도 캐시합니다.<br /><br /> 데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스를 위한 사용자 그룹에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
#### <a name="notes"></a>참고  
  
-   SharePoint 팜에 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 응용 프로그램 파일, 데이터 파일 및 속성을 콘텐츠 데이터베이스와 서비스 응용 프로그램 데이터베이스에 저장합니다.  
  
-   기존 설치에 기능을 추가할 경우 이전에 설치한 기능의 위치를 변경하거나 새 기능의 위치를 지정할 수 없습니다.  

-   SQL Server 폴더 및 파일 형식을 제외하도록 바이러스 백신 및 스파이웨어 방지 응용 프로그램과 같은 검색 소프트웨어를 구성해야 할 수도 있습니다. 자세한 내용은 [SQL Server를 실행하는 컴퓨터에서 바이러스 백신 소프트웨어](https://support.microsoft.com/kb/309422) 지원 문서를 검토하세요.
  
-   기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소도 별도의 디렉터리에 설치해야 합니다.  
  
-   다음과 같은 위치에는 프로그램 파일 및 데이터 파일을 설치할 수 없습니다.  
  
    -   이동식 디스크 드라이브  
  
    -   압축 파일 시스템  
  
    -   시스템 파일이 있는 디렉터리  
  
#### <a name="see-also"></a>관련 항목:  
 디렉터리, 파일 위치 및 인스턴스 ID 명명에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.  
  
    
 [파일 서버의 공유 및 NTFS 권한](http://go.microsoft.com/fwlink/?LinkID=206571) 

## <a name="database-engine-configuration---filestream"></a>데이터베이스 엔진 구성 - Filestream
  이 페이지를 사용하여 이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치에 대해 FILESTREAM을 사용하도록 설정할 수 있습니다. FILESTREAM은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] varbinary(max) **BLOB(Binary Large Object) 데이터를 파일 시스템의 파일로 저장하여** 을 NTFS 파일 시스템과 통합합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 FILESTREAM 데이터를 삽입, 업데이트, 쿼리, 검색 및 백업할 수 있습니다. Win32 파일 시스템 인터페이스에서는 데이터에 대한 스트리밍 액세스를 제공합니다.  
  
### <a name="uielement-list"></a>UIElement 목록  
 **Transact-SQL 액세스에 FILESTREAM 사용**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정하려면 선택합니다. 다른 컨트롤 옵션을 사용하려면 먼저 이 컨트롤을 선택해야 합니다.  
  
 **파일 I/O 스트리밍 액세스에 FILESTREAM 사용**  
 Win32 스트리밍 액세스에 FILESTREAM을 사용하도록 설정하려면 선택합니다.  
  
 **Windows 공유 이름**  
 FILESTREAM 데이터가 저장될 Windows 공유의 이름을 입력하려면 이 컨트롤을 사용합니다.  
  
 **원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스를 가질 수 있도록 허용**  
 원격 클라이언트가 이 서버의 이 FILESTREAM 데이터에 액세스할 수 있도록 허용하려면 이 컨트롤을 선택합니다.  
  
### <a name="see-also"></a>관련 항목:  
 [FILESTREAM 사용 및 구성](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

  
## <a name="database-engine-configuration---server-configuration"></a>데이터베이스 엔진 구성 - 서버 구성
  이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 모드를 설정하고 Windows 사용자 또는 그룹을 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 관리자로 추가할 수 있습니다.  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 실행 고려 사항  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **BUILTIN\Administrators** 그룹이 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 로그인으로 프로비전되었으며 로컬 관리자 그룹의 멤버는 해당 관리자 자격 증명을 사용하여 로그인할 수 있었습니다. 그러나 높은 권한은 가급적 사용하지 않는 것이 좋으므로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 **BUILTIN\Administrators** 그룹이 로그인으로 프로비전되어 있지 않습니다. 따라서 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치하는 동안 각 관리자에 대해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로그인을 만들고 이 로그인을 sysadmin 고정 서버 역할에 추가해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업(복제 에이전트 작업 포함)을 실행하는 데 사용되는 Windows 계정에 대해서도 이 작업을 수행해야 합니다.  
  
### <a name="options"></a>옵션  
 **보안 모드** - 설치에 사용할 인증(Windows 인증 또는 혼합 모드 인증)을 선택합니다.  
  
 **Windows 보안 주체 프로비전** - 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 Windows Builtin\Administrator 로컬 그룹이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 서버 역할에 배치되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 액세스 권한이 사실상 Windows 관리자에게 부여되었습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 Builtin\Administrator 그룹은 sysadmin 서버 역할로 프로비전되지 않습니다. 대신 설치 중에 새 설치에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자를 명시적으로 프로비전해야 합니다.  
  
> [!IMPORTANT]  
>  설치 중에 새 설치에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자를 명시적으로 프로비전해야 합니다. 이 단계를 완료해야 설치 프로그램이 다음 단계로 진행됩니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 지정** - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 Windows 보안 주체를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 실행되는 계정을 추가하려면 **현재 사용자** 단추를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
 목록 편집을 마치면 **확인**을 클릭한 다음 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다.  
  
 혼합 모드 인증을 선택한 경우 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SA(시스템 관리자) 계정에 대해 로그온 자격 증명을 제공해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows 인증 모드**  
 사용자가 Microsoft Windows 사용자 계정을 통해 연결되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 운영 체제의 Windows 보안 주체 토큰을 사용하여 계정 이름과 암호가 유효한지 확인합니다. 이것은 기본 인증 모드이며 혼합 모드보다 훨씬 더 안전합니다. Windows 인증은 Kerberos 보안 프로토콜을 사용하고, 암호 정책을 적용하여 강력한 암호에 대해 적합한 복잡성 수준을 유지하도록 하며, 계정 잠금 및 암호 만료를 지원합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 비어 있거나 약한 sa 암호는 설정하지 마십시오.  
  
 **혼합 모드(Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증)**  
 사용자가 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결할 수 있도록 허용합니다. Windows 사용자 계정을 통해 연결하는 사용자는 Windows에서 유효성을 검사하는 트러스트된 연결을 사용할 수 있습니다.  
  
 혼합 모드 인증을 선택해야 하며 레거시 응용 프로그램을 수용하기 위해 SQL 로그인을 사용해야 할 경우 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정에 대해 강력한 암호를 설정해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 오로지 이전 버전과의 호환성을 위해서만 제공됩니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **암호 입력**  
 시스템 관리자(sa) 로그인을 입력하고 확인하십시오. 암호는 침입을 막는 최전방 방어선이므로 시스템 보안을 위해서는 반드시 강력한 암호를 설정해야 합니다. 빈 암호나 약한 sa 암호로는 설정하지 마십시오.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호는 문자, 기호 및 숫자를 임의로 조합하여 1자에서 128자까지 포함할 수 있습니다. 혼합 모드 인증을 선택한 경우 설치 마법사의 다음 페이지로 이동하기 전에 강력한 sa 암호를 입력해야 합니다.  
  
 **강력한 암호 지침**  
 강력한 암호는 쉽게 추측할 수 없으며 컴퓨터 프로그램을 사용하여 해킹하기도 어렵습니다. 강력한 암호에는 다음을 비롯한 금지된 조건 및 용어를 사용할 수 없습니다.  
  
-   빈 조건 또는 NULL 조건  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 강력한 암호에는 설치 컴퓨터와 관련된 다음 용어를 사용할 수 없습니다.  
  
-   컴퓨터에 현재 로그온한 사용자의 이름  
  
-   컴퓨터 이름  
  
 강력한 암호는 8자 이상이어야 하며 다음의 네 가지 조건 중 세 가지 이상을 만족해야 합니다.  
  
-   대문자를 포함해야 합니다.  
  
-   소문자를 포함해야 합니다.  
  
-   숫자를 포함해야 합니다.  
  
-   #, % 또는 ^과 같은 비영숫자를 포함해야 합니다.  
  
 이 페이지에 입력하는 암호는 강력한 암호 정책 요구 사항을 만족해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 자동화가 있으면 암호가 강력한 암호 정책 요구 사항을 만족하는지 확인하십시오.  
  
### <a name="related-content"></a>관련 내용  
 Windows 인증과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 중 어느 것을 선택할지 알아보려면 [인증 모드 선택](../../relational-databases/security/choose-an-authentication-mode.md)을 참조하세요.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 실행할 계정을 선택하는 방법에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.
  
## <a name="database-engine-configuration---tempdb"></a>데이터베이스 엔진 구성 - TempDB
  이 페이지를 사용하여 **tempdb** 데이터와 로그 파일의 크기, 위치, 증가 설정 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]의 파일 수를 지정합니다. 설치 유형에 따라 지원되는 저장소에 로컬 디스크, 공유 저장소 또는 SMB 파일 서버가 포함될 수 있습니다.  
  
 SMB 파일 공유를 디렉터리로 지정하려면 지원되는 UNC 경로를 수동으로 입력해야 합니다. SMB 파일 공유를 찾아볼 수는 없습니다. SMB 파일 공유에 지원되는 UNC 경로 형식은 \\\Servername\ShareName\\....입니다.  
  
### <a name="data-and-log-directories-for--a-stand-alone-instance-of--includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스의 데이터 및 로그 디렉터리  
 다음 표에는 설치 중 사용자가 구성할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에 지원되는 저장소 유형 및 기본 디렉터리가 나열되어 있습니다.  
  
|설명|지원되는 저장소 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**데이터 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 저장소* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.<br /><br /> **temdb** 디렉터리의 모범 사례는 작업 및 성능 요구 사항에 따라 달라집니다. 여러 볼륨에 데이터 파일을 나눌 여러 폴더/드라이버를 지정합니다.|  
|**로그 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 저장소*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
  
 *공유 디스크가 지원되기는 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에는 사용하지 않는 것이 좋습니다.  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스의 데이터 및 로그 디렉터리  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스에 대한 지원되는 저장소 유형 및 기본 디렉터리를 보여 줍니다.  
  
|설명|지원되는 저장소 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**tempdb** 데이터 디렉터리|로컬 디스크, 공유 저장소, SMB 파일 서버|\<드라이브:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\Data<br /><br /> 팁: **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.<br /><br /> 지정된 디렉터리(여러 파일이 지정된 경우 여러 디렉터리)가 모든 클러스터 노드에 대해 유효한지 확인합니다. 장애 조치(Failover) 중에 장애 조치(Failover) 대상 노드에서 **tempdb** 디렉터리를 사용할 수 없으면 SQL Server 리소스가 온라인이 될 수 없습니다.|  
|**tempdb** 로그 디렉터리|로컬 디스크, 공유 저장소, SMB 파일 서버|\<드라이브:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> 팁: **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 공유 디스크가 선택되어 있지 않은 경우 이 필드는 기본적으로 비어 있습니다.|사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.<br /><br /> 지정한 디렉터리가 모든 클러스터 노드에 유효한지 확인하십시오. 장애 조치(Failover) 중에 장애 조치(Failover) 대상 노드에서 **tempdb** 디렉터리를 사용할 수 없으면 SQL Server 리소스가 온라인이 될 수 없습니다.<br /><br /> 로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
  
### <a name="uielement-list"></a>UIElement 목록  
 작업 및 요구 사항에 따라 **tempdb** 설정을 구성합니다. 다음 설정은 **tempdb** 데이터 파일에 적용됩니다.  
  
-   **파일 수** 는 **tempdb**의 데이터 파일의 총 수입니다. 기본값은 8과 설정에서 감지한 논리 코어 수 중 작은 수입니다. 일반적으로 논리 프로세서의 수가 8 이하인 경우 논리 프로세서와 같은 수의 데이터 파일을 사용합니다. 논리 프로세서의 수가 8보다 클 경우 8개의 데이터 파일을 사용합니다. 그런 다음에도 경합이 계속될 경우 경합이 허용 가능한 수준으로 감소할 때까지 데이터 파일의 수를 4의 배수로 늘리거나 작업/코드를 변경합니다. 
  
-   **초기 크기(MB)** 는 각 **tempdb** 데이터 파일의 초기 크기(MB 단위)입니다. 기본값은 8MB(또는 [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]의 경우 4MB)입니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]에서는 초기 최대 파일 크기가 262,144MB(256GB)입니다. [!INCLUDE[sssql15](../../includes/sssql15-md.md)]의 초기 최대 파일 크기는 1,024MB였습니다. 모든 **tempdb** 데이터 파일의 초기 크기는 동일합니다. SQL Server가 시작되거나 장애 조치(failover)할 때마다 **tempdb** 가 생성되므로 일반 작업에 필요한 크기와 가까운 크기를 지정해야 합니다. 시작 시 **tempdb** 생성을 최적화하려면 [데이터베이스 즉시 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 사용하도록 설정합니다.  
  
-   **총 초기 크기(MB)** 는 모든 **tempdb** 데이터 파일의 누적 크기입니다.  
  
-   **자동 증가(MB)** 는 공간이 부족해질 때 각 **tempdb** 데이터 파일이 자동으로 증가하는 공간의 양(메가바이트 단위)입니다. [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 및 이후 버전에서는 모든 데이터 파일이 이 설정에서 지정한 양만큼 동시에 증가합니다.  
  
-   **총 자동 증가(MB)** 는 각 자동 증가 이벤트의 누적 크기입니다.  
  
-   **데이터 디렉터리** 에는 **tempdb** 데이터 파일이 저장된 모든 디렉터리가 표시됩니다. 여러 디렉터리가 있는 경우에는 데이터 파일이 디렉터리에 라운드 로빈 방식으로 배치됩니다. 예를 들어 3개의 디렉터리를 만들고 8개의 데이터 파일을 지정하는 경우 1, 4, 7번 데이터 파일이 첫 번째 디렉터리에 생성됩니다. 2, 5, 8번 데이터 파일은 두 번째 디렉터리에 생성됩니다. 3, 6번 데이터 파일은 세 번째 디렉터리에 생성됩니다.  
  
-   디렉터리를 추가하려면 **추가...**를 클릭합니다.  
  
-   디렉터리를 제거하려면 디렉터리를 선택하고 **제거**를 클릭합니다.  
  
 **TempDB 로그 파일** 은 로그 파일의 이름이며 자동으로 생성됩니다. 다음 설정은 **tempdb** 로그 파일에만 적용됩니다.  
  
-   **초기 크기(MB)** 는 **tempdb** 로그 파일의 초기 크기입니다. 기본값은 8MB(또는 [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]의 경우 4MB)입니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]에서는 초기 최대 파일 크기가 262,144MB(256GB)입니다. [!INCLUDE[sssql15](../../includes/sssql15-md.md)]의 초기 최대 파일 크기는 1,024MB였습니다. SQL Server가 시작되거나 장애 조치(failover)할 때마다 **tempdb** 가 생성되므로 일반 작업에 필요한 크기와 가까운 크기를 지정해야 합니다. 시작 시 **tempdb** 생성을 최적화하려면 [데이터베이스 즉시 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 사용하도록 설정합니다.  
  
-   **참고: Tempdb** 는 최소한의 로깅을 사용합니다. **tempdb** 로그는 백업할 수 없으며 SQL Server가 시작되거나 클러스터 인스턴스가 장애 조치(failover)될 때마다 다시 생성됩니다.  
  
-   **자동 증가(MB)** 는 **tempdb** 로그의 증가 증분(메가바이트 단위)입니다.  기본값인 64MB에서는 초기화 중 최적의 가상 로그 파일 수가 생성됩니다.  
  
-   **참고: Tempdb** 로그 파일은 인스턴트 파일 초기화를 사용하지 않습니다.  
  
-   **로그 디렉터리** 는 **tempdb** 로그 파일이 생성되는 디렉터리입니다. **tempdb** 로그 디렉터리는 하나뿐입니다.  
  
### <a name="security-considerations"></a>보안 고려 사항  
 설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.  

 SMB 파일 서버에는 다음과 같은 권장 사항이 적용됩니다.  
  
-   SMB 파일 서버가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정은 도메인 계정이어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정은 데이터 디렉터리로 사용되는 SMB 파일 공유 폴더에 대해 FULL CONTROL NTFS 권한이 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정에는 SMB 파일 서버에 대한 SeSecurityPrivilege 권한이 부여되어야 합니다. 이 권한을 부여하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 계정을 **감사 및 보안 로그 관리** 정책에 추가합니다. 이 설정은 **로컬 보안 정책** 콘솔의 **로컬 정책** 에 있는 **사용자 권한 지정** 섹션에서 사용할 수 있습니다.  
  
### <a name="notes"></a>참고  
  
-   기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소도 별도의 디렉터리에 설치해야 합니다.  
  
### <a name="see-also"></a>관련 항목:  
 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [파일 서버의 공유 및 NTFS 권한](http://go.microsoft.com/fwlink/?LinkID=206571)  

## <a name="database-engine-configuration---user-instance"></a>데이터베이스 엔진 구성 - 사용자 인스턴스
**사용자 인스턴스** 페이지를 사용하여 관리자 권한 없이 사용자에 대한 개별 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 생성하고 관리자 역할에 사용자를 추가할 수 있습니다.  
  
### <a name="option"></a>옵션  
 사용자 인스턴스 활성화  
 이 옵션은 기본적으로 사용됩니다. 사용자 인스턴스 활성화 기능을 비활성화하려면 확인란의 선택을 취소하십시오.  
  
 자식 인스턴스 또는 클라이언트 인스턴스라고도 하는 사용자 인스턴스는 부모 인스턴스( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같이 서비스로 실행되는 주 인스턴스)가 사용자 대신 생성하는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]인스턴스입니다. 사용자 인스턴스는 해당 사용자의 보안 컨텍스트에서 사용자 프로세스로 실행됩니다. 사용자 인스턴스는 부모 인스턴스 및 컴퓨터에서 실행되는 그 밖의 사용자 인스턴스로부터 격리됩니다. 사용자 인스턴스 기능을 "RANU(일반 사용자로 실행)"라고도 합니다.  
  
> [!NOTE]  
>  설치 중에 **sysadmin** 고정 서버 역할의 멤버로 프로비전되는 로그인은 템플릿 데이터베이스에서 관리자로 프로비전됩니다. 이들은 제거되는 경우가 아니면 사용자 인스턴스에서 **sysadmin** 고정 서버 역할의 멤버가 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 역할에 사용자 추가  
 이 옵션은 기본적으로 사용되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 역할에 현재 설치 사용자를 추가하려면 확인란을 선택하십시오.  
  
 BUILTIN\Administrators의 멤버인 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 사용자는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 연결할 때 sysadmin 고정 서버 역할에 자동으로 추가되지 않습니다. 서버 수준의 관리자 역할에 명시적으로 추가된 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 사용자만 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 관리할 수 있습니다. Built-In\Users 그룹의 멤버는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스에 연결할 수 있지만 제한적인 데이터베이스 태스크 수행 권한을 가집니다. 따라서 이전 Windows 릴리스의 BUILTIN\Administrators 및 Built-In\Users에서 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 권한을 상속받은 사용자는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 에서 실행하는 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]인스턴스에서 관리 권한을 명시적으로 부여 받아야 합니다.  
  
 이 설치 프로그램이 끝난 후 사용자 역할을 변경하려면 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 노출 영역 구성 도구(SQLSAC.exe)를 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 역할의 사용자 목록을 업데이트하려면 **새 관리자 추가** 링크를 클릭합니다.  
  
 **제공할 사용자** 필드에 권한이 업데이트되어야 할 사용자의 DomainName\UserName이 나열되어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 가능한 권한 **창에 있는** 인스턴스 목록에서 업데이트할 역할을 선택한 다음 오른쪽 화살표를 클릭합니다. 사용 가능한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 역할에 사용자를 추가하려면 오른쪽 화살표를 두 번 클릭합니다.  
  
 선택 작업이 완료된 경우 변경 내용을 구현하려면 [!INCLUDE[clickOK](../../includes/clickok-md.md)]. 변경 없이 도구를 끝내려면 **취소**를 클릭합니다.  
  
  

