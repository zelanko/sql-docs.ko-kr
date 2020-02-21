---
title: 설치 마법사 도움말 | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: b32ad209651c30f810f239b0c14689be497c4378
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69609296"
---
# <a name="installation-wizard-help"></a>설치 마법사 도움말

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사의 일부 구성 페이지에 대해 설명합니다.

## <a name="instance-configuration-page"></a>인스턴스 구성 페이지

**설치 마법사의** 인스턴스 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 만들지 또는 명명된 인스턴스를 만들지 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 아직 설치되지 않은 경우 명명된 인스턴스를 지정하지 않으면 기본 인스턴스가 만들어집니다.  
  
각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 특정 데이터 정렬과 기타 옵션이 지정된 고유의 서비스 집합으로 구성됩니다. 디렉터리 구조, 레지스트리 구조 및 서비스 이름은 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 생성된 인스턴스 이름과 특정 인스턴스 ID를 반영합니다.  
  
인스턴스는 기본 인스턴스이거나 명명된 인스턴스입니다. 기본 인스턴스 이름은 MSSQLSERVER입니다. 기본 이름을 사용하면 클라이언트가 연결할 때 인스턴스 이름을 지정하지 않아도 됩니다. 명명된 인스턴스는 설치 중 사용자가 결정합니다. 기본 인스턴스를 먼저 설치하지 않고도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 명명된 인스턴스로 설치할 수 있습니다. 버전과 관계없이 한 번에 하나의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치만 기본 인스턴스가 될 수 있습니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용할 경우 **인스턴스 구성** 페이지에서 준비 인스턴스를 완료할 때 인스턴스 이름을 지정할 수 있습니다. 머신에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스가 없는 경우 완료 중인 준비 인스턴스를 기본 인스턴스로 구성할 수 있습니다.  
  
### <a name="multiple-instances"></a>여러 인스턴스
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 단일 서버 또는 프로세서에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지원하지만 하나의 인스턴스만 기본 인스턴스가 될 수 있습니다. 다른 모든 인스턴스는 명명된 인스턴스여야 합니다. 한 컴퓨터에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 동시에 실행할 수 있으며, 각 인스턴스가 다른 인스턴스와는 별도로 실행됩니다.  
  
 자세한 내용은 [SQL Server의 최대 용량 사양](../maximum-capacity-specifications-for-sql-server.md)을 참조하세요.  
  
### <a name="options"></a>옵션

**장애 조치(Failover) 클러스터 인스턴스만**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 네트워크 이름을 지정합니다. 이 이름은 네트워크에서 장애 조치(Failover) 클러스터 인스턴스를 식별합니다.  
  
**기본 인스턴스 또는 명명된 인스턴스 중에서 선택**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스 또는 명명된 인스턴스를 설치할 것인지 결정하는 경우 다음 정보를 고려합니다.  
  
* 데이터베이스 서버에 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치할 경우 이 인스턴스는 기본 인스턴스여야 합니다.  
  
* 동일한 컴퓨터에 여러 인스턴스를 설치할 경우에는 명명된 인스턴스를 사용합니다. 한 서버에서 기본 인스턴스 한 개만 호스팅할 수 있습니다.  
* [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 를 설치하는 애플리케이션은 이를 명명된 인스턴스로 설치해야 합니다. 이렇게 하면 여러 애플리케이션을 동일한 컴퓨터에 설치한 경우 충돌을 최소화할 수 있습니다.
  
**기본 인스턴스**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스를 설치하려면 이 옵션을 선택합니다. 한 컴퓨터에서는 기본 인스턴스를 하나만 호스팅할 수 있으며 나머지 인스턴스는 모두 명명된 인스턴스여야 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 인스턴스가 설치되어 있으면 동일한 컴퓨터에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 인스턴스를 추가할 수 있습니다.  
  
**명명된 인스턴스**: 새 명명된 인스턴스를 만들려는 경우 이 옵션을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 이름을 지정하는 경우 다음 정보에 유의하세요.  
  
* 인스턴스 이름은 대/소문자를 구분하지 않습니다.  
  
* 인스턴스 이름은 밑줄(_)로 시작하거나 끝날 수 없습니다.  
  
* 인스턴스 이름에 “Default” 용어나 다른 예약 키워드를 사용할 수 없습니다. 인스턴스 이름에 예약 키워드를 사용하면 설치 오류가 발생합니다. 자세한 내용은 [예약 키워드&#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)를 참조하세요.  
  
* 인스턴스 이름으로 MSSQLSERVER를 지정하면 기본 인스턴스가 만들어집니다.  
  
* [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 설치는 항상 “[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]”의 명명된 인스턴스로 설치됩니다. 이 기능 역할에는 다른 인스턴스 이름을 지정할 수 없습니다.  
  
* 인스턴스 이름은 16자로 제한됩니다.  
  
* 인스턴스 이름의 첫 글자는 문자여야 합니다. 허용되는 문자는 유니코드 표준 2.0에서 정의된 문자입니다. 이러한 문자에는 라틴어 문자 a-z와 A-Z, 다른 언어의 문자가 포함됩니다.  
  
* 이어지는 글자는 유니코드 표준 2.0에 정의된 문자, 기본 라틴어 또는 기타 국가별 스크립트에 정의된 숫자, 달러 기호($) 또는 밑줄(_)이 될 수 있습니다.  
  
* 포함된 공백이나 다른 특수 문자는 인스턴스 이름에 사용할 수 없습니다. 백슬래시(\\), 쉼표(,), 콜론(:), 세미콜론(;), 작은따옴표(‘), 앰퍼샌드(&), 하이픈(-) 및 @ 기호도 사용할 수 없습니다.  
  
  현재 Windows 코드 페이지에서 유효한 문자만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름에 사용할 수 있습니다. 지원되지 않는 유니코드 문자를 사용하면 설치 오류가 발생합니다.  
  
**감지된 인스턴스 및 기능**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 실행 중인 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 구성 요소 목록을 확인합니다.  
  
**인스턴스 ID**: 기본적으로 인스턴스 이름이 인스턴스 ID로 사용됩니다. 이 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 설치 디렉터리 및 레지스트리 키를 식별하는 데 사용됩니다. 동일한 동작이 기본 인스턴스와 명명된 인스턴스에 모두 적용됩니다. 기본 인스턴스의 경우, 인스턴스 이름과 인스턴스 ID는 MSSQLSERVER입니다. 기본값이 아닌 인스턴스 ID를 사용하려면 **인스턴스 ID** 필드에 해당 ID를 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep을 사용할 경우 **인스턴스 구성** 페이지에 표시되는 인스턴스 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 프로세스의 이미지 준비 단계 중에 지정한 인스턴스 ID입니다. 이미지 완료 단계에서는 다른 인스턴스 ID를 지정할 수 없습니다.

> [!NOTE]  
>  밑줄(_)로 시작하거나 숫자 기호(#) 또는 달러 기호($)가 포함된 인스턴스 ID는 지원되지 않습니다.  
  
디렉터리, 파일 위치 및 인스턴스 ID 명명에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.  
  
지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 구성 요소는 하나의 단위로 관리됩니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 팩과 업그레이드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 구성 요소에 적용됩니다.  
  
같은 인스턴스 이름을 공유하는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 다음 조건을 충족해야 합니다.  
  
* 같은 버전
* 같은 에디션
* 같은 언어 설정
* 같은 클러스터형 상태
* 같은 운영 체제  
  
> [!NOTE]  
> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 클러스터를 인식하지 않습니다.  

## <a name="analysis-services-configuration---account-provisioning-page"></a>Analysis Services 구성 - 계정 프로비저닝 페이지
  
이 페이지를 사용하여 서버 모드를 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 제한 없이 액세스해야 하는 사용자나 서비스에 관리 권한을 부여할 수 있습니다. 설치할 인스턴스의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 관리자 역할에 로컬 Windows 그룹 BUILTIN\Administrators가 자동으로 추가되지 않습니다. 로컬 Administrators 그룹을 서버 관리자 역할에 추가하려면 해당 그룹을 명시적으로 지정해야 합니다.  
  
[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 시에는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 팜에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 배포를 담당하는 SharePoint 팜 관리자 또는 서비스 관리자에게 관리 권한을 부여해야 합니다.  
  
### <a name="options"></a>옵션

**서버 모드**: 서버 모드는 서버에 배포할 수 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 유형을 지정합니다. 서버 모드는 설치 중에 결정되며 나중에 수정할 수 없습니다. 각 모드는 함께 사용할 수 없습니다. 즉, 클래식 OLAP(온라인 분석 처리) 및 테이블 형식 모델 솔루션을 모두 지원하려면 각각 서로 다른 모드에 맞게 구성된 두 개의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 필요합니다.  
  
**관리자 지정**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 서버 관리자를 한 명 이상 지정해야 합니다. 지정한 사용자 또는 그룹은 설치할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 서버 관리자 역할 구성원이 됩니다. 이러한 구성원은 소프트웨어를 설치할 컴퓨터와 동일한 도메인에 Windows 도메인 사용자 계정이 있어야 합니다.  
  
> [!NOTE]  
> UAC(사용자 계정 컨트롤)는 관리 작업이나 애플리케이션을 실행하기 전에 관리자가 구체적으로 승인해야 하는 Windows 보안 기능입니다. UAC는 기본적으로 켜져 있으므로, 상승된 권한이 필요한 특정 작업을 허용하라는 메시지가 표시됩니다. UAC를 구성하여 기본 동작을 변경하거나, 특정 프로그램에 맞게 UAC를 사용자 지정할 수 있습니다. UAC 및 UAC 구성에 대한 자세한 내용은 [사용자 계정 컨트롤 단계별 가이드](https://go.microsoft.com/fwlink/?linkid=196350) 및 [사용자 계정 컨트롤(Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351)을 참조하세요.  
  
### <a name="see-also"></a>참고 항목
  
* [서비스 계정 구성&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services)
* [Windows 서비스 계정 및 사용 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  

## <a name="analysis-services-configuration---data-directories-page"></a>Analysis Services 구성 - 데이터 디렉터리 페이지

다음 표의 기본 디렉터리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있습니다. 이러한 파일에 대한 액세스 권한은 설치 중에 만들어져 프로비저닝되는 SQLServerMSASUser$\<instance> 보안 그룹의 구성원과 로컬 관리자에게 부여됩니다.  
  
### <a name="uielement-list"></a>UIElement 목록  
  
|Description|기본 디렉터리|권장 사항|  
|-----------------|-----------------------|---------------------|  
|**데이터 루트 디렉터리**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data\ |\Program files\Microsoft SQL Server\ 폴더가 제한된 권한으로 보호되어 있는지 확인하십시오. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 성능은 대부분의 구성에서 데이터 디렉터리가 있는 스토리지의 성능에 따라 달라집니다. 이 디렉터리는 시스템에 연결된 성능이 가장 높은 스토리지에 배치합니다. 장애 조치(Failover) 클러스터 설치의 경우 공유 디스크에 데이터 디렉터리를 만들어야 합니다.|  
|**로그 파일 디렉터리**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log\ |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그 파일에 사용되며 FlightRecorder 로그를 포함합니다. 비행 레코더 기간을 늘려야 하는 경우 로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|**임시 디렉터리**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp\ |임시 디렉터리도 성능이 뛰어난 스토리지 하위 시스템에 배치합니다.|  
|**백업 디렉터리**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup\ |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 백업 파일에 사용됩니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 시에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 파일도 이 디렉터리에 캐시합니다.<br /><br /> 데이터 손실을 방지하고, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 사용자 그룹에 백업 디렉터리에 대한 충분한 쓰기 권한이 있도록 적절한 사용 권한이 설정되었는지 확인합니다. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
### <a name="considerations"></a>고려 사항  
  
* SharePoint 팜에 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 애플리케이션 파일, 데이터 파일 및 속성을 콘텐츠 데이터베이스와 서비스 애플리케이션 데이터베이스에 저장합니다.  
  
* 기존 설치에 기능을 추가하는 경우 이전에 설치한 기능의 위치를 변경하거나 새 기능의 위치를 지정할 수 없습니다.  

* SQL Server 폴더 및 파일 형식을 제외하도록 바이러스 백신 및 스파이웨어 방지 애플리케이션과 같은 검색 소프트웨어를 구성해야 할 수도 있습니다. 자세한 내용은 다음 지원 문서를 검토하세요. [SQL Server를 실행하는 컴퓨터의 바이러스 백신 소프트웨어](https://support.microsoft.com/kb/309422).
  
* 기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 디렉터리를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 디렉터리와 공유하지 마세요. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소를 설치하여 디렉터리를 구분합니다.  
  
* 다음과 같은 위치에는 프로그램 파일과 데이터 파일을 설치할 수 없습니다.  
  
  * 이동식 디스크 드라이브  
  * 압축 파일 시스템  
  * 시스템 파일이 있는 디렉터리  
  
### <a name="see-also"></a>참고 항목

디렉터리, 파일 위치 및 인스턴스 ID 명명에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.  
  
### <a name="analysis-services-configuration---data-directories-page"></a>Analysis Services 구성 - 데이터 디렉터리 페이지

다음 표의 기본 디렉터리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 사용자가 구성할 수 있습니다. 이러한 파일에 대한 액세스 권한은 설치 중에 만들어져 프로비저닝되는 SQLServerMSASUser$\<instance> 보안 그룹의 구성원과 로컬 관리자에게 부여됩니다.  
  
#### <a name="uielement-list"></a>UIElement 목록
  
|Description|기본 디렉터리|권장 사항|  
|-----------------|-----------------------|---------------------|  
|**데이터 루트 디렉터리** |\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data |\Program files\Microsoft SQL Server\ 폴더가 제한된 권한으로 보호되어 있는지 확인하십시오. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 성능은 대부분의 구성에서 데이터 디렉터리가 있는 스토리지의 성능에 따라 달라집니다. 이 디렉터리는 시스템에 연결된 성능이 가장 높은 스토리지에 배치합니다. 장애 조치(Failover) 클러스터 설치의 경우 공유 디스크에 데이터 디렉터리를 배치해야 합니다.|  
|**로그 파일 디렉터리**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그 파일에 사용되며 FlightRecorder 로그를 포함합니다. 비행 레코더 기간을 늘리는 경우 로그 디렉터리에 충분한 공간이 있는지 확인합니다.|  
|**임시 디렉터리**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp |임시 디렉터리도 성능이 뛰어난 스토리지 하위 시스템에 배치합니다.|  
|**백업 디렉터리**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup |이 디렉터리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 기본 백업 파일에 사용됩니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 시에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 파일도 이 디렉터리에 캐시합니다.<br /><br /> 데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스를 위한 사용자 그룹에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
#### <a name="considerations"></a>고려 사항
  
* SharePoint 팜에 배포된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 애플리케이션 파일, 데이터 파일 및 속성을 콘텐츠 데이터베이스와 서비스 애플리케이션 데이터베이스에 저장합니다.  
  
* 기존 설치에 기능을 추가하는 경우 이전에 설치한 기능의 위치를 변경하거나 새 기능의 위치를 지정할 수 없습니다.  

* SQL Server 폴더 및 파일 형식을 제외하도록 바이러스 백신 및 스파이웨어 방지 애플리케이션과 같은 검색 소프트웨어를 구성해야 할 수도 있습니다. 자세한 내용은 [SQL Server를 실행하는 컴퓨터의 바이러스 백신 소프트웨어](https://support.microsoft.com/kb/309422)를 참조하세요.
  
* 기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 디렉터리를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 디렉터리와 공유하지 마세요. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소를 설치하여 디렉터리를 구분합니다.  
  
* 다음과 같은 위치에는 프로그램 파일과 데이터 파일을 설치할 수 없습니다.  
  
  * 이동식 디스크 드라이브  
  * 압축 파일 시스템  
  * 시스템 파일이 있는 디렉터리  
  
#### <a name="see-also"></a>참고 항목

* 디렉터리, 파일 위치 및 인스턴스 ID 명명에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하세요.  
* [파일 서버의 공유 및 NTFS 권한](https://docs.microsoft.com/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)

## <a name="serverconfig"></a> 데이터베이스 엔진 구성 - 서버 구성 페이지

이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 모드를 설정하고 Windows 사용자 또는 그룹을 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 관리자로 추가할 수 있습니다.  
  
### <a name="considerations-for-running-sscurrent"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 실행 고려 사항

이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 BUILTIN\Administrators 그룹이 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 로그인으로 프로비저닝되었으며, 로컬 관리자 그룹의 구성원이 해당 관리자 자격 증명을 사용하여 로그인할 수 있었습니다. 그러나 상승된 권한은 가급적 사용하지 않는 것이 좋습니다.

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 BUILTIN\Administrators 그룹이 로그인으로 프로비저닝되어 있지 않습니다. 새 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스를 설치하는 동안 각 관리자에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만들고 이 로그인을 **sysadmin** 고정 서버 역할에 추가해야 합니다. 복제 에이전트 작업을 포함하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 실행하는 Windows 계정에도 동일한 작업을 수행합니다.  
  
### <a name="options"></a>옵션

**보안 모드**: 설치에 대해 **Windows 인증** 또는 **혼합 모드 인증**을 선택합니다.  
  
**Windows 보안 주체 프로비저닝**: 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 Windows BUILTIN\Administrators 로컬 그룹이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** 서버 역할에 배치되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 권한이 사실상 Windows 관리자에게 부여되었습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 BUILTIN\Administrators 그룹이 **sysadmin** 서버 역할에 프로비저닝되어 있지 않습니다. 대신 설치 중에 새 설치에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자를 명시적으로 프로비전해야 합니다.  
  
> [!IMPORTANT]  
> 설치 중에 새 설치에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자를 명시적으로 프로비전해야 합니다. 이 단계를 완료해야 설치를 계속할 수 있습니다.
  
**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 지정**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 Windows 보안 주체를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행 중인 계정을 추가하려면 **현재 사용자 추가** 단추를 선택합니다. 시스템 관리자 목록에서 계정을 추가하거나 제거하려면 **추가** 또는 **제거**를 선택한 다음, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자 권한이 있는 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
목록 편집을 마쳤으면 **확인**을 선택하고, 구성 대화 상자에서 관리자 목록을 확인합니다. 목록이 완료되었으면 **다음**을 선택합니다.  
  
**혼합 모드 인증**을 선택한 경우 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**sa**(시스템 관리자) 계정에 대해 로그인 자격 증명을 제공해야 합니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
**Windows 인증 모드**: 사용자가 Microsoft Windows 사용자 계정을 통해 연결되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 운영 체제의 Windows 보안 주체 토큰을 사용하여 계정 이름과 암호가 유효한지 확인합니다. Windows 인증이 기본 인증 모드이며, 혼합 모드 인증보다 훨씬 더 안전합니다. Windows 인증은 Kerberos 보안 프로토콜을 사용하고, 암호 정책을 적용하여 강력한 암호에 적합한 복잡성 수준을 유지하도록 하며, 계정 잠금 및 암호 만료를 지원합니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  

> [!IMPORTANT]  
> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 비어 있거나 약한 **sa** 암호를 설정하지 마세요.  
  
**혼합 모드(Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증)** : 사용자가 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결할 수 있도록 허용합니다. Windows 사용자 계정을 통해 연결하는 사용자는 Windows에서 유효성을 검사하는 트러스트된 연결을 사용할 수 있습니다.  
  
혼합 모드 인증을 선택해야 하고 레거시 애플리케이션을 수용하기 위해 SQL 로그인을 사용해야 하는 경우, 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정에 대해 강력한 암호를 설정해야 합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 이전 버전과의 호환성을 위해서만 제공됩니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
**암호 입력**: 시스템 관리자(**sa**) 로그인을 입력하고 확인합니다. 암호는 침입을 막는 최전방 방어선이므로 시스템 보안을 위해서는 반드시 강력한 암호를 설정해야 합니다. 비어 있거나 약한 **sa** 암호를 설정하지 마세요.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호는 문자, 기호 및 숫자를 임의로 조합하여 1자에서 128자까지 포함할 수 있습니다. 혼합 모드 인증을 선택한 경우 설치 마법사의 다음 페이지로 넘어가기 전에 강력한 **sa** 암호를 입력해야 합니다.  
  
#### <a name="strong-password-guidelines"></a>강력한 암호 지침
  
강력한 암호는 쉽게 추측할 수 없으며 컴퓨터 프로그램을 사용하여 해킹하기도 어렵습니다. 강력한 암호에는 다음을 비롯한 금지된 조건이나 용어를 사용할 수 없습니다.  
  
* 빈 조건 또는 NULL 조건
* "Password"
* "Admin"
* "Administrator"
* "sa"
* "sysadmin"

강력한 암호에는 설치 컴퓨터와 관련된 다음 용어를 사용할 수 없습니다.  
  
* 머신에 현재 로그인한 사용자의 이름
* 컴퓨터 이름  
  
강력한 암호는 8자 이상이어야 하며 다음의 네 가지 조건 중 세 가지 이상을 만족해야 합니다.  
  
* 대문자를 포함해야 합니다.
* 소문자를 포함해야 합니다.  
* 숫자를 포함해야 합니다.
* #, % 또는 ^과 같은 비영숫자를 포함해야 합니다.  
  
이 페이지에 입력하는 암호는 강력한 암호 정책 요구 사항을 충족해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 자동화가 있는 경우, 암호가 강력한 암호 정책 요구 사항을 충족하는지 확인합니다.  
  
### <a name="see-also"></a>참고 항목

Windows 인증과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 중에서 하나를 선택하는 방법에 대한 자세한 내용은 [인증 모드 선택](../../relational-databases/security/choose-an-authentication-mode.md)을 참조하세요.  

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 실행할 계정을 선택하는 방법에 대한 자세한 내용은 [Windows 서비스 계정 및 사용 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.

## <a name ="datadir"></a> 데이터베이스 엔진 구성 - 데이터 디렉터리 페이지

이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로그램과 데이터 파일의 설치 위치를 지정할 수 있습니다. 설치 유형에 따라 지원되는 스토리지에 로컬 디스크, 공유 스토리지 또는 SMB 파일 서버가 포함될 수 있습니다.  
  
SMB 파일 공유를 디렉터리로 지정하려면 지원되는 UNC 경로를 수동으로 입력해야 합니다. SMB 파일 공유를 찾아볼 수 없습니다. 다음 예제에서는 SMB 파일 공유에 대해 지원되는 UNC 경로 형식을 보여 줍니다.

`\\<ServerName>\<ShareName>\...`

### <a name="standalone-instance-of-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스
  
다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에서 지원되는 스토리지 유형 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 구성할 수 있는 기본 디렉터리가 나와 있습니다.  
  
### <a name="uielement-list"></a>UIElement 목록
  
|Description|지원되는 스토리지 형식|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**데이터 루트 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 스토리지* |\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL(액세스 제어 목록)을 구성하고 상속을 중단합니다.|  
|**사용자 데이터베이스 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 스토리지*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data |사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.|  
|**사용자 데이터베이스 로그 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 스토리지*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|**백업 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 스토리지*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup|데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 위한 사용자 계정에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
\* 공유 디스크가 지원되기는 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에는 사용하지 않는 것이 좋습니다.  
  
### <a name="failover-cluster-instance-of-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스

다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스에서 지원되는 스토리지 유형 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 구성할 수 있는 기본 디렉터리가 나와 있습니다.  
  
|Description|지원되는 스토리지 형식|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**데이터 루트 디렉터리**|공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> **팁**: **클러스터 디스크 선택** 페이지에서 **공유 디스크**를 선택하는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 디스크를 선택하지 않으면 이 필드는 기본적으로 비어 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 중단합니다.|  
|**사용자 데이터베이스 디렉터리**|공유 스토리지, SMB 파일 서버|\<Drive:>Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> **팁**: **클러스터 디스크 선택** 페이지에서 **공유 디스크**를 선택하는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 디스크를 선택하지 않으면 이 필드는 기본적으로 비어 있습니다.|사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.|  
|**사용자 데이터베이스 로그 디렉터리**|공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> **팁**: **클러스터 디스크 선택** 페이지에서 **공유 디스크**를 선택하는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 디스크를 선택하지 않으면 이 필드는 기본적으로 비어 있습니다.|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
|**백업 디렉터리**|로컬 디스크, 공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup<br /><br /> **팁**: **클러스터 디스크 선택** 페이지에서 **공유 디스크**를 선택하는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 디스크를 선택하지 않으면 이 필드는 기본적으로 비어 있습니다.|데이터 손실을 방지할 수 있도록 적절한 권한을 설정하고 SQL Server 서비스를 위한 사용자 계정에 백업 디렉터리에 대한 적절한 쓰기 권한이 있는지 확인하십시오. 백업 디렉터리에는 매핑된 드라이브를 사용할 수 없습니다.|  
  
### <a name="security-considerations"></a>보안 고려 사항
  
설치 프로그램은 구성 과정 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 해제합니다.  
  
SMB 파일 서버에는 다음과 같은 권장 사항이 적용됩니다.  
  
* SMB 파일 서버가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정은 도메인 계정이어야 합니다.  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정은 데이터 디렉터리로 사용되는 SMB 파일 공유 폴더에 대해 모든 권한 NTFS 권한이 있어야 합니다.  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정에는 SMB 파일 서버에 대한 SeSecurityPrivilege 권한이 부여되어야 합니다. 이 권한을 부여하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 계정을 **감사 및 보안 로그 관리** 정책에 추가합니다. 이 설정은 로컬 보안 정책 콘솔에서 **로컬 정책** 아래의 **사용자 권한 할당** 섹션에 있습니다.

### <a name="considerations"></a>고려 사항
  
* 기존 설치에 기능을 추가하는 경우 이전에 설치한 기능의 위치를 변경하거나 새 기능의 위치를 지정할 수 없습니다.  
  
* 기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 디렉터리를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 디렉터리와 공유하지 마세요. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소를 설치하여 디렉터리를 구분합니다.  
  
* 다음과 같은 위치에는 프로그램 파일과 데이터 파일을 설치할 수 없습니다.  
  
  * 이동식 디스크 드라이브
  * 압축 파일 시스템
  * 시스템 파일이 있는 디렉터리
  * 장애 조치(failover) 클러스터 인스턴스의 매핑된 네트워크 드라이브  
  
## <a name="a-nametempdba-database-engine-configuration---tempdb-page"></a><a name="tempdb"><a/> 데이터베이스 엔진 구성 - TempDB 페이지

이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 **tempdb** 데이터 및 로그 파일 위치, 크기, 증가 설정, 파일 수를 지정할 수 있습니다. 설치 유형에 따라 지원되는 스토리지에 로컬 디스크, 공유 스토리지 또는 SMB 파일 서버가 포함될 수 있습니다.  
  
SMB 파일 공유를 디렉터리로 지정하려면 지원되는 UNC 경로를 수동으로 입력해야 합니다. SMB 파일 공유를 찾아볼 수 없습니다. 다음 예제에서는 SMB 파일 공유에 대해 지원되는 UNC 경로 형식을 보여 줍니다.

`\\<ServerName>\<ShareName>\....`
  
### <a name="data-and-log-directories-for-a-standalone-instance-of-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 독립 실행형 인스턴스의 데이터 및 로그 디렉터리

다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에 대해 지원되는 스토리지 유형 및 설치 중에 구성할 수 있는 기본 디렉터리가 나와 있습니다.  
  
|Description|지원되는 스토리지 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**데이터 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 스토리지* |\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 중단합니다.<br /><br /> **tempdb** 디렉터리의 모범 사례는 워크로드 및 성능 요구 사항에 따라 달라집니다. 여러 볼륨에 데이터 파일을 분산하려면 여러 폴더 또는 드라이버를 지정합니다.|  
|**로그 디렉터리**|로컬 디스크, SMB 파일 서버, 공유 스토리지*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
  
\* 공유 디스크가 지원되기는 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 독립 실행형 인스턴스에는 사용하지 않는 것이 좋습니다.  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스의 데이터 및 로그 디렉터리

다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 장애 조치(failover) 클러스터 인스턴스에서 지원되는 스토리지 유형 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 구성할 수 있는 기본 디렉터리가 나와 있습니다.  
  
|Description|지원되는 스토리지 유형|기본 디렉터리|권장 사항|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**tempdb 데이터 디렉터리**|로컬 디스크, 공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\Data<br /><br /> **팁**: **클러스터 디스크 선택** 페이지에서 **공유 디스크**를 선택하는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 디스크를 선택하지 않으면 이 필드는 기본적으로 비어 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 구성 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 중단합니다.<br /><br /> 지정한 디렉터리(여러 파일을 지정한 경우 여러 디렉터리)가 모든 클러스터 노드에 유효한지 확인합니다. 장애 조치(failover) 중에, 장애 조치(failover) 대상 노드에서 **tempdb** 디렉터리를 사용할 수 없는 경우 SQL Server 리소스가 온라인 상태로 전환되지 않습니다.|  
|**tempdb 로그 디렉터리**|로컬 디스크, 공유 스토리지, SMB 파일 서버|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> **팁**: **클러스터 디스크 선택** 페이지에서 **공유 디스크**를 선택하는 경우 기본값은 첫 번째 공유 디스크입니다. **클러스터 디스크 선택** 페이지에 디스크를 선택하지 않으면 이 필드는 기본적으로 비어 있습니다.|사용자 데이터 디렉터리에 대한 모범 지침은 작업 및 성능 요구 사항에 따라 달라집니다.<br /><br /> 지정한 디렉터리가 모든 클러스터 노드에 유효한지 확인하십시오. 장애 조치(failover) 중에, 장애 조치(failover) 대상 노드에서 **tempdb** 디렉터리를 사용할 수 없는 경우 SQL Server 리소스가 온라인 상태로 전환되지 않습니다.<br /><br /> 로그 디렉터리에 적절한 공간이 있는지 확인하십시오.|  
  
### <a name="uielement-list"></a>UIElement 목록

작업 및 요구 사항에 따라 **tempdb** 설정을 구성합니다. 다음 설정은 **tempdb** 데이터 파일에 적용됩니다.  
  
* **파일 수** 는 **tempdb**의 데이터 파일의 총 수입니다. 기본값은 설치 프로그램에서 검색한 논리 코어 수와 8 중에서 작은 값입니다. 일반적으로 논리 프로세서의 수가 8 이하인 경우 논리 프로세서와 같은 수의 데이터 파일을 사용합니다. 논리 프로세서 수가 8보다 크면 8개의 데이터 파일을 사용합니다. 경합이 발생할 경우, 경합이 허용 가능한 수준으로 감소할 때까지 데이터 파일 수를 논리 프로세서 수까지 4의 배수로 늘리거나, 워크로드 또는 코드를 변경합니다.
  
* **초기 크기(MB)** 는 각 **tempdb** 데이터 파일의 초기 크기(메가바이트)입니다. 기본값은 8MB(또는 [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]의 경우 4MB)입니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]에서는 초기 최대 파일 크기가 262,144MB(256GB)입니다. [!INCLUDE[sssql15](../../includes/sssql15-md.md)]의 최대 초기 파일 크기는 1024MB입니다. 모든 **tempdb** 데이터 파일의 초기 크기는 동일합니다. SQL Server를 시작하거나 장애 조치(failover)할 때마다 **tempdb**가 다시 생성되므로 일반 작업의 워크로드에 필요한 크기에 가까운 크기를 지정합니다. 시작 시 **tempdb** 생성을 더 최적화하려면 [데이터베이스 즉시 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 사용하도록 설정합니다.  
  
* **총 초기 크기(MB)** 는 모든 **tempdb** 데이터 파일의 누적 크기입니다.  
  
* **자동 증가(MB)** 는 공간이 부족할 때 각 **tempdb** 데이터 파일이 자동으로 증가하는 공간 크기(메가바이트)입니다. [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 이상에서는 모든 데이터 파일이 이 설정에 지정된 크기만큼 동시에 증가합니다.  
  
* **총 자동 증가(MB)** 는 각 자동 증가 이벤트의 누적 크기입니다.  
* **데이터 디렉터리**에는 **tempdb** 데이터 파일이 저장된 모든 디렉터리가 표시됩니다. 여러 디렉터리가 있는 경우에는 데이터 파일이 디렉터리에 라운드 로빈 방식으로 배치됩니다. 예를 들어 디렉터리 3개를 만들고 데이터 파일 8개를 지정하는 경우 데이터 파일 1, 4, 7이 첫 번째 디렉터리에 생성됩니다. 데이터 파일 2, 5, 8은 두 번째 디렉터리에 생성됩니다. 데이터 파일 3, 6은 세 번째 디렉터리에 생성됩니다.  
  
* 디렉터리를 추가하려면 **추가...** 를 선택합니다.  
  
* 디렉터리를 제거하려면 해당 디렉터리를 선택하고 **제거**를 선택합니다.  
  
**TempDB 로그 파일**은 로그 파일의 이름입니다. 이 파일은 자동으로 생성됩니다. 다음 설정은 **tempdb** 로그 파일에만 적용됩니다.  
  
* **초기 크기(MB)** 는 **tempdb** 로그 파일의 초기 크기입니다. 기본값은 8MB(또는 [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]의 경우 4MB)입니다. [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]에서는 초기 최대 파일 크기가 262,144MB(256GB)입니다. [!INCLUDE[sssql15](../../includes/sssql15-md.md)]의 최대 초기 파일 크기는 1024MB입니다. SQL Server를 시작하거나 장애 조치(failover)할 때마다 **tempdb**가 다시 생성되므로 일반 작업의 워크로드에 필요한 크기에 가까운 크기를 지정합니다. 시작 시 **tempdb** 생성을 더 최적화하려면 [데이터베이스 즉시 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 사용하도록 설정합니다.  
  
  > [!NOTE]
  > **Tempdb**는 최소한의 로깅을 사용합니다. **tempdb** 로그 파일은 백업할 수 없으며 SQL Server를 시작하거나 클러스터 인스턴스를 장애 조치(failover)할 때마다 다시 생성됩니다.

* **자동 증가(MB)** 는 **tempdb** 로그의 증가 증분(메가바이트 단위)입니다.  기본값인 64MB에서는 초기화 중 최적의 가상 로그 파일 수가 생성됩니다.  

  > [!NOTE]
  > **Tempdb** 로그 파일은 데이터베이스 즉시 파일 초기화를 사용하지 않습니다.
  
* **로그 디렉터리** 는 **tempdb** 로그 파일이 생성되는 디렉터리입니다. **tempdb** 로그 디렉터리는 하나뿐입니다.  
  
### <a name="security-considerations"></a>보안 고려 사항
  
설치 프로그램은 구성 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리에 대한 ACL을 구성하고 상속을 중단합니다.  

SMB 파일 서버에는 다음과 같은 권장 사항이 적용됩니다.  
  
* SMB 파일 서버가 사용되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정은 도메인 계정이어야 합니다.  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정은 데이터 디렉터리로 사용되는 SMB 파일 공유 폴더에 대해 **모든 권한** NTFS 권한이 있어야 합니다.  
  
* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 사용되는 계정에는 SMB 파일 서버에 대한 SeSecurityPrivilege 권한이 부여되어야 합니다. 이 권한을 부여하려면 파일 서버의 로컬 보안 정책 콘솔을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 계정을 **감사 및 보안 로그 관리** 정책에 추가합니다. 이 설정은 로컬 보안 정책 콘솔에서 **로컬 정책** 아래의 **사용자 권한 할당** 섹션에 있습니다.  
  
> [!NOTE]
> 기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 고유한지 확인해야 합니다. 이 대화 상자의 어떠한 디렉터리도 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 디렉터리와 공유되지 않아야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소도 별도의 디렉터리에 설치해야 합니다.
  
### <a name="see-also"></a>참고 항목

* [Windows 서비스 계정 및 사용 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).
* [파일 서버의 공유 및 NTFS 권한](https://docs.microsoft.com/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)  

<!--
The MaxDOP setting applies only to SQL Server 2019 and later.
-->

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="a-namemaxdopa-database-engine-configuration---maxdop-page"></a><a name="maxdop"><a/> 데이터베이스 엔진 구성 - MaxDOP 페이지

**MaxDOP(최대 병렬 처리 수준)** 는 단일 문이 사용할 수 있는 최대 프로세서 수를 결정합니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 설치 중에 이 옵션을 구성하는 기능이 도입되었습니다. 또한 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서는 코어 수에 따라 서버에 권장되는 MaxDOP 설정을 자동으로 검색합니다.  

설치하는 동안 이 페이지를 건너뛰면 기본 MaxDOP 값은 이전 버전 (0)의 기본 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 대신 이 페이지에 표시되는 권장 값입니다. 이 페이지에서는 이 설정을 수동으로 구성할 수도 있으며, 설치 후에 이 설정을 수정할 수 있습니다. 

### <a name="uielement-list"></a>UIElement 목록

* **MaxDOP(최대 병렬 처리 수준)** 는 단일 문을 병렬로 실행하는 동안 사용할 최대 프로세서 수에 대 한 값입니다. 기본값은 [최대 병렬 처리 수준 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)의 최대 병렬 처리 수준 지침에 따라 정렬됩니다.

## <a name="a-namememorya-database-engine-configuration---memory-page"></a><a name="memory"><a/> 데이터베이스 엔진 구성 - 메모리 페이지

**최소 서버 메모리**는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]가 버퍼 풀 및 기타 캐시에 대해 사용할 낮은 메모리 제한을 결정합니다. 기본값과 및 권장되는 값은 모두 0입니다. **최소 서버 메모리**의 효과에 대한 자세한 내용은 [메모리 관리 아키텍처 가이드](../../relational-databases/memory-management-architecture-guide.md#effects-of-min-and-max-server-memory)를 참조하세요.

**최소 서버 메모리**는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]가 버퍼 풀 및 기타 캐시에 대해 사용할 높은 메모리 제한을 결정합니다. 기본값은 2,147,483,647MB(메가바이트)이며 계산 된 권장값은 기존 시스템 메모리를 기반으로 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)의 메모리 구성 지침에 따라 정렬됩니다. **최대 서버 메모리**의 효과에 대한 자세한 내용은 [메모리 관리 아키텍처 가이드](../../relational-databases/memory-management-architecture-guide.md#effects-of-min-and-max-server-memory)를 참조하세요.

설치하는 동안이 페이지를 건너뛰면 사용된 기본 **최대 서버 메모리** 값이 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 기본값(2,147,483,647메가바이트)입니다. **권장** 라디오 단추를 선택하면 이 페이지에서 이러한 설정을 수동으로 구성할 수 있으며 설치 후에 수정할 수 있습니다. 자세한 내용은 [Server Memory Configuration Options](../../database-engine/configure-windows/server-memory-server-configuration-options.md)(서버 메모리 구성 옵션)를 참고하세요.

### <a name="uielement-list"></a>UIElement 목록
  
**기본값**: 이 라디오 단추는 기본적으로 선택되어 있으며 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 기본값에 대한 **최소 서버 메모리** 및 **최대 서버 메모리** 설정으로 설정되어 있습니다. 

**권장**: 계산된 권장 값을 수락하거나 계산된 값을 사용자 구성 값으로 변경하려면 이 라디오 단추를 선택해야 합니다.  
  
**최소 서버 메모리(MB)** : 계산된 권장 값에서 사용자 구성 값으로 변경하는 경우 **최소 서버 메모리**에 대한 값을 입력합니다.  
  
**최대 서버 메모리(MB)** : 계산된 권장 값에서 사용자 구성 값으로 변경하는 경우 **최대 서버 메모리**에 대한 값을 입력합니다.  

**SQL Server Database Engine에 권장되는 메모리 구성을 적용하려면 여기 클릭**: 이 서버에서 계산된 권장 메모리 구성을 적용하려면 이 확인란을 선택합니다. **권장** 라디오 단추를 선택한 경우 이 확인란을 선택하지 않으면 설치를 계속할 수 없습니다.

::: moniker-end

## <a name="database-engine-configuration---filestream-page"></a>데이터베이스 엔진 구성 - FILESTREAM 페이지

이 페이지를 사용하여 이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치에 대해 FILESTREAM을 사용하도록 설정할 수 있습니다. FILESTREAM은 **varbinary(max)** BLOB(Binary Large Object) 데이터를 파일 시스템의 파일로 저장하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 NTFS 파일 시스템과 통합합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 FILESTREAM 데이터를 삽입, 업데이트, 쿼리, 검색 및 백업할 수 있습니다. Microsoft Win32 파일 시스템 인터페이스는 데이터에 대한 스트리밍 액세스를 제공합니다. 
  
### <a name="uielement-list"></a>UIElement 목록
  
**Transact-SQL 액세스에 FILESTREAM 사용**: [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스에 FILESTREAM을 사용하도록 설정하려면 선택합니다. 이 확인란을 먼저 선택해야 다른 옵션을 사용할 수 있습니다.  
  
**파일 I/O 스트리밍 액세스에 FILESTREAM 사용**: Win32 스트리밍 액세스에 FILESTREAM을 사용하도록 설정하려면 선택합니다.  
  
**Windows 공유 이름**: FILESTREAM 데이터를 저장할 Windows 공유의 이름을 입력합니다.  
  
**원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스를 가질 수 있도록 허용**: 원격 클라이언트가 이 서버의 FILESTREAM 데이터에 액세스할 수 있도록 허용하려면 이 확인란을 선택합니다.  
  
### <a name="see-also"></a>참고 항목

* [FILESTREAM 사용 및 구성](../../relational-databases/blob/enable-and-configure-filestream.md)
* [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

## <a name="database-engine-configuration---user-instance-page"></a>데이터베이스 엔진 구성 - 사용자 인스턴스 페이지

**사용자 인스턴스** 페이지를 사용하여 다음을 수행할 수 있습니다.

* 관리자 권한이 없는 사용자를 위해 별도의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 생성합니다.
* 관리자 역할에 사용자를 추가합니다.  
  
### <a name="options"></a>옵션
  
**사용자 인스턴스 사용**: 기본값은 ON입니다. 사용자 인스턴스를 사용하도록 설정하는 기능을 끄려면 확인란 선택을 취소합니다.  
  
자식 인스턴스 또는 클라이언트 인스턴스라고도 하는 사용자 인스턴스는 부모 인스턴스( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같이 서비스로 실행되는 주 인스턴스)가 사용자 대신 생성하는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]인스턴스입니다. 사용자 인스턴스는 해당 사용자의 보안 컨텍스트에서 사용자 프로세스로 실행됩니다. 사용자 인스턴스는 부모 인스턴스 및 컴퓨터에서 실행 중인 다른 모든 사용자 인스턴스로부터 격리됩니다. 사용자 인스턴스 기능을 “RANU(일반 사용자로 실행)”라고도 합니다.  
  
> [!NOTE]  
> 설치 중에 **sysadmin** 고정 서버 역할의 구성원으로 프로비저닝된 로그인은 템플릿 데이터베이스에서 관리자로 프로비저닝됩니다. 제거하는 않는 한, 사용자 인스턴스에서 **sysadmin** 고정 서버 역할의 구성원이 됩니다.  
  
**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 역할에 사용자 추가**:  기본값은 OFF입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 역할에 현재 설치 프로그램 사용자를 추가하려면 확인란을 선택합니다.  
  
BUILTIN\Administrators의 구성원인 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 사용자는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 연결할 때 **sysadmin** 고정 서버 역할에 자동으로 추가되지 않습니다. 서버 수준의 관리자 역할에 명시적으로 추가된 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 사용자만 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 관리할 수 있습니다. Built-In\Users 그룹의 구성원은 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스에 연결할 수 있지만 데이터베이스 작업 수행 권한이 제한됩니다. 따라서 이전 Windows 릴리스의 BUILTIN\Administrators 및 Built-In\Users에서 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 권한을 상속받은 사용자는 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]에서 실행 중인 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스에서 관리 권한을 명시적으로 부여받아야 합니다.  
  
설치 프로그램이 종료된 후 사용자 역할을 변경하려면 [SQL Server Management Studio](../../relational-databases/security/authentication-access/join-a-role.md) 또는 [Transact-SQL](../../t-sql/statements/alter-role-transact-sql.md)을 사용합니다.
