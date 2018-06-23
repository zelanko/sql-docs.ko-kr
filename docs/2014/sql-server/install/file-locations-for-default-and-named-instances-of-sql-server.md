---
title: SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 463c570e-9f75-4653-b3b8-4d61753b0013
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0b20fee2459dfb9273abe4e43b79ff76fdfe2dfc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091665"
---
# <a name="file-locations-for-default-and-named-instances-of-sql-server"></a>SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치는 하나 이상의 개별 인스턴스로 구성됩니다. 기본 인스턴스인지 또는 명명된 인스턴스인지에 관계없이 인스턴스에는 컴퓨터의 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 공유되는 공용 파일 집합 외에 고유의 프로그램과 데이터 파일 집합이 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssDE](../../includes/ssde-md.md)]및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 포함하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]인스턴스의 경우 각 구성 요소는 데이터와 실행 파일, 그리고 컴퓨터에서 공유하는 공통 파일을 모두 가지고 있습니다.  
  
 각 구성 요소의 설치 위치를 분리하기 위해 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 내의 각 구성 요소에 대해 고유한 인스턴스 ID가 생성됩니다.  
  
> [!IMPORTANT]  
>  프로그램 파일 및 데이터 파일은 이동식 디스크 드라이브, 압축을 사용하는 파일 시스템, 시스템 파일이 있는 디렉터리 및 장애 조치(Failover) 클러스터 인스턴스에 있는 공유 드라이브에 설치할 수 없습니다.  
>   
>  시스템 데이터베이스(master, model, MSDB 및 tempdb)와 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 사용자 데이터베이스는 SMB(서버 메시지 블록) 파일 서버에 저장소 옵션으로 설치될 수 있습니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 독립 실행형 설치와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 설치) 모두에 적용됩니다. 자세한 내용은 [Install SQL Server with SMB Fileshare as a Storage Option](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)를 참조하세요.  
>   
>  Binn, Data, Ftdata, HTML 또는 1033 디렉터리나 포함된 내용을 삭제하지 마세요. 필요한 경우 다른 디렉터리는 삭제할 수 있지만 삭제된 기능이나 데이터를 검색하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제거했다가 다시 설치해야 합니다. HTML 디렉터리의 .htm 파일을 삭제하거나 수정하지 마십시오. 이 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구가 올바르게 동작하는 데 필요합니다.  
  
## <a name="shared-files-for-all-instances-of-includessnoversionincludesssnoversion-mdmd"></a>모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 단일 컴퓨터의 모든 인스턴스에 사용되는 공용 파일은 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)] 폴더에 설치됩니다. 여기서 \<*drive*>는 구성 요소가 설치된 드라이브 문자입니다. 기본값은 일반적으로 C 드라이브입니다.  
  
## <a name="file-locations-and-registry-mapping"></a>파일 위치 및 레지스트리 매핑  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 각 서버 구성 요소에 대한 인스턴스 ID가 생성됩니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스의 서버 구성 요소는 [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]입니다.  
  
 기본 인스턴스 ID는 다음 형식을 사용하여 구성됩니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]인 경우 MSSQL이 제일 먼저 나오고 다음에 주 버전 번호, 밑줄과 부 버전(해당되는 경우), 마침표, 인스턴스 이름이 차례로 나옵니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인 경우 MSAS가 제일 먼저 나오고 다음에 주 버전 번호, 밑줄과 부 버전(해당되는 경우), 마침표, 인스턴스 이름이 차례로 나옵니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]인 경우 MSRS가 제일 먼저 나오고 다음에 주 버전 번호, 밑줄과 부 버전(해당되는 경우), 마침표, 인스턴스 이름이 차례로 나옵니다.  
  
 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 사용되는 기본 인스턴스 ID의 예는 다음과 같습니다.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 기본 인스턴스인 경우 MSSQL12.MSSQLSERVER  
  
-   [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]의 기본 인스턴스인 경우 MSAS12.MSSQLSERVER  
  
-   "MyInstance"로 명명된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스인 경우 MSSQL12.MyInstance  
  
 "MyInstance"로 명명된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 과 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 를 포함하고 기본 디렉터리에 설치된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 명명된 인스턴스에 대한 디렉터리 구조는 다음과 같습니다.  
  
-   C:\Program Files\Microsoft SQL Server\MSSQL12.MyInstance\  
  
-   C:\Program Files\Microsoft SQL Server\MSAS12.MyInstance\  
  
 인스턴스 ID에는 어떤 값이든 자유롭게 지정할 수 있지만 특수 문자와 예약 키워드는 사용하지 마십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 기본 인스턴스 ID가 아닌 인스턴스 ID를 지정할 수 있습니다. 사용자가 기본 설치 디렉터리를 변경하도록 선택하는 경우에는 \<Program Files>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대신 \<사용자 지정 경로>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 사용됩니다. 밑줄(_)로 시작되거나 숫자 기호(#) 또는 달러 기호($)가 들어 있는 인스턴스 ID는 지원되지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 클라이언트 구성 요소는 인스턴스 인식형이 아니므로 인스턴스 ID가 할당되지 않습니다. 기본적으로 인스턴스 비인식형 구성 요소는 단일 디렉터리 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]에 설치됩니다. 한 공유 구성 요소의 설치 경로를 변경하면 다른 공유 구성 요소의 설치 경로도 변경됩니다. 후속 설치 시 원래 설치와 동일한 디렉터리에 인스턴스 비인식형 구성 요소가 설치됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 설치 후 인스턴스 이름 변경을 지원하는 유일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소입니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 이름을 바꾸어도 인스턴스 ID는 변경되지 않습니다. 인스턴스 이름을 바꾼 후에도 디렉터리 및 레지스트리 키는 설치 중에 만든 인스턴스 ID를 계속 사용합니다.  
  
 인스턴스 인식형 구성 요소인 경우 레지스트리 하이브는 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*Instance_ID*> 아래에 생성됩니다. 예:  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\ 합니다. MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\msas12.<instanceid>\olap\config\ 합니다. MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12 합니다. MyInstance  
  
 레지스트리는 또한 인스턴스 이름과 인스턴스 ID의 매핑을 유지 관리합니다. 인스턴스 이름과 인스턴스 ID의 매핑은 다음과 같이 유지 관리됩니다.  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\SQL] "InstanceName"="MSSQL12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\OLAP] "InstanceName"="MSAS12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\RS] "InstanceName"="MSRS12"  
  
## <a name="specifying-file-paths"></a>파일 경로 지정  
 설치 중에 다음 기능에 대한 설치 경로를 변경할 수 있습니다.  
  
 설치 경로는 사용자 구성 대상 폴더가 있는 기능에 대해서만 설치 프로그램에 표시됩니다.  
  
|구성 요소|기본 경로<sup>1, 2</sup>|구성 가능한<sup>3</sup> 또는 고정 경로|  
|---------------|---------------------------------|--------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 서버 구성 요소|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\.\< InstanceID >\|구성 가능|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 데이터 파일|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\.\< InstanceID >\|구성 가능|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\msas12.<instanceid>\olap\config\.\< InstanceID >\|구성 가능|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 파일|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\msas12.<instanceid>\olap\config\.\< InstanceID >\|구성 가능|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12.\< InstanceID > services\reportserver\bin\|구성 가능|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 관리자|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12.\< InstanceID > services\reportmanager\|고정된 경로|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|\<설치 디렉터리 > \120\DTS\|구성 가능한<sup>4</sup>|  
|클라이언트 구성 요소(bcp.exe 및 sqlcmd.exe 제외)|\<설치 디렉터리 > \120\Tools\|구성 가능한<sup>4</sup>|  
|클라이언트 구성 요소(bcp.exe 및 sqlcmd.exe 제외)|\<설치 디렉터리>\Client SDK\ODBC\110\Tools\Binn|고정 경로|  
|복제 및 서버 쪽 COM 개체|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\\<sup>5</sup>|고정 경로|  
|데이터 변환 런타임 엔진, 데이터 변환 파이프라인 엔진 및 `dtexec` 명령 프롬프트 유틸리티에 대한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소 DLL|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|고정 경로|  
|에 대해 관리되는 연결을 지원하는 DLL(!!) [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Connections|고정 경로|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 지원하는 각 열거자 유형에 대한 DLL|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\ForEachEnumerators|고정 경로|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스, WMI 공급자|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]공유\|고정된 경로|  
|의 모든 인스턴스 간에 공유되는 구성 요소(!!) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]공유\|고정된 경로|  
  
 <sup>1</sup>\Program files 확인\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ 폴더가 제한 된 권한으로 보호 됩니다.  
  
 <sup>2</sup>이러한 위치의 기본 드라이브는 *systemdrive*이며 일반적으로 C 드라이브입니다.  
  
 <sup>3</sup>하위 기능에 대 한 설치 경로 상위 기능의 설치 경로에 따라 달라 집니다.  
  
 <sup>4</sup>간에 단일 설치 경로가 공유 됩니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 클라이언트 구성 요소입니다. 한 구성 요소의 설치 경로를 변경하면 다른 구성 요소에 대한 설치 경로도 변경됩니다. 후속 설치 시 원래 설치와 동일한 위치에 구성 요소를 설치합니다.  
  
 <sup>5</sup>이 디렉터리의 모든 인스턴스가 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 있습니다. 컴퓨터의 모든 인스턴스에 업데이트를 적용할 경우 이 폴더의 파일 내용을 변경하면 모든 인스턴스에 적용됩니다. 기존 설치에 기능을 추가할 경우 이전에 설치한 기능의 위치를 변경하거나 새 기능의 위치를 지정할 수 없습니다. 설치 프로그램에서 이미 설정한 디렉터리에 추가 기능을 설치하거나 제품을 제거했다가 다시 설치해야 합니다.  
  
> [!NOTE]  
>  클러스터형 구성의 경우 클러스터의 각 노드에서 사용할 수 있는 로컬 드라이브를 선택해야 합니다.  
  
 설치 중에 서버 구성 요소나 데이터 파일의 설치 경로를 지정하면 설치 프로그램은 프로그램 및 데이터 파일에 대해 지정된 위치 외에 인스턴스 ID를 사용합니다. 설치 프로그램은 도구 및 기타 공유 파일에 대해 인스턴스 ID를 사용하지 않습니다. 또한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 리포지토리에 대해서는 인스턴스 ID를 사용하지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로그램 및 데이터 파일에 대해서는 인스턴스 ID를 사용하지 않습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 기능에 대한 설치 경로를 설정한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 해당 경로를 해당 설치(SQL 데이터 파일 포함)의 모든 인스턴스별 폴더에 대한 루트 디렉터리로 사용합니다. 이 경우 루트를 설정한 경우 "C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\.\< 인스턴스 이름 > \MSSQL\\", 인스턴스별 디렉터리가 경로 끝에 추가 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사(설치 UI 모드)에서 USESYSDB 업그레이드 기능을 사용하는 경우에는 하위 폴더가 반복 포함된 구조로 제품이 설치될 수 있습니다. 예를 들어 \< *SQLProgramFiles*> \MSSQL12\MSSQL\MSSQL10_50\MSSQL\Data\\합니다. USESYSDB 기능을 사용하려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 기능 대신 SQL 데이터 파일 기능에 대한 설치 경로를 설정합니다.  
  
> [!NOTE]  
>  데이터 파일은 항상 Data라는 하위 디렉터리에 위치합니다. 예를 들어 C:\Program Files 지정\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\.\< 인스턴스 이름 > \ \ 데이터 파일이 C:\Program Files 아래에 나와 있는 경우 업그레이드 하는 동안 루트 경로를 시스템 데이터베이스의 데이터 디렉터리로 지정 하려면\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\.\< 인스턴스 이름 > \MSSQL\Data 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 구성 - 데이터 디렉터리](../../../2014/sql-server/install/database-engine-configuration-data-directories.md)   
 [Analysis Services 구성 - 데이터 디렉터리](../../../2014/sql-server/install/analysis-services-configuration-data-directories.md)  
  
  