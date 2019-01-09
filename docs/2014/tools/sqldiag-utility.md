---
title: SQLdiag 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], SQLdiag
- stopping diagnostic collection
- storing diagnostic information
- performance [SQL Server], diagnostic collection
- diagnostic records [SQL Server]
- scripts [SQL Server], diagnostic collection
- logs [SQL Server], diagnostic collection
- starting diagnostic collection
- clustered instance of SQL Server
- monitoring performance [SQL Server], diagnostic collection
- security [SQL Server], diagnostic collection
- SQLDIAG service
- space [SQL Server], diagnostic collection
- SQLdiag utility
- disk space [SQL Server], diagnostic collection
- configuration files [SQL Server]
- automatic diagnostic collection
- clusters [SQL Server], diagnostic collection
ms.assetid: 45ba1307-33d1-431e-872c-a6e4556f5ff2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a024e2fc4cb7afaecdc6e84ae6dba4f3a2700d8b
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590257"
---
# <a name="sqldiag-utility"></a>SQLdiag Utility
  **SQLdiag** 유틸리티는 콘솔 응용 프로그램 또는 서비스로 실행할 수 있는 범용 진단 정보 수집 유틸리티입니다. **SQLdiag** 를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 기타 서버 유형에서 로그 및 데이터 파일을 수집할 수 있으며 이러한 파일을 사용하여 지속적으로 서버를 모니터링하거나 특정 서버 문제를 해결할 수 있습니다. **SQLdiag** 는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 고객 지원 서비스에서 진단 정보를 빠르고 간편하게 수집할 수 있도록 지원하는 유틸리티입니다.  
  
> [!NOTE]  
>  이 유틸리티는 변경될 수 있으며 해당 명령줄 인수나 동작을 사용하는 애플리케이션 또는 스크립트의 경우 후속 릴리스에서 제대로 작동하지 않을 수 있습니다.  
  
 **SQLdiag** 에서는 다음과 같은 진단 정보를 수집할 수 있습니다.  
  
-   Windows 성능 로그  
  
-   Windows 이벤트 로그  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 추적 정보  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 차단 정보  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 정보  
  
 SQLDiag.xml 구성 파일을 편집하여 **SQLdiag** 에서 수집할 정보 유형을 지정할 수 있습니다. 이에 대해서는 다음 섹션에서 설명합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      sqldiag   
     { [/?] }  
     |  
     { [/I configuration_file]  
       [/O output_folder_path]  
       [/Psupport_folder_path]  
       [/Noutput_folder_management_option]  
       [/Mmachine1 [ machine2machineN]| @machinelistfile]  
       [/Cfile_compression_type]  
       [/B [+]start_time]  
       [/E [+]stop_time]  
       [/ASQLdiag_application_name]  
       [/T { tcp [ ,port ] | np | lpc } ]  
       [/Q] [/G] [/R] [/U] [/L] [/X] }  
     |  
     { [START | STOP | STOP_ABORT] }  
     |  
     { [START | STOP | STOP_ABORT] /ASQLdiag_application_name }  
```  
  
## <a name="arguments"></a>인수  
 **/?**  
 사용법 정보를 표시합니다.  
  
 **/I** _configuration_file_  
 **SQLdiag** 에서 사용할 구성 파일을 설정합니다. 기본적으로 **/I** 는 SQLDiag.Xml로 설정되어 있습니다.  
  
 **/O** _output_folder_path_  
 **SQLdiag** 출력을 지정된 폴더로 리디렉션합니다. **/O** 옵션을 지정하지 않으면 **SQLdiag** 출력이 **SQLdiag** 시작 폴더의 SQLDIAG라는 하위 폴더에 기록됩니다. SQLDIAG 폴더가 없으면 **SQLdiag** 에서 이 폴더를 만듭니다.  
  
> [!NOTE]  
>  출력 폴더 위치는 **/P**로 지정할 수 있는 지원 폴더 위치에 대해 상대적입니다. 완전히 다른 출력 폴더 위치를 설정하려면 **/O**에 대해 전체 디렉터리 경로를 지정합니다.  
  
 **/P** _support_folder_path_  
 지원 폴더 경로를 설정합니다. 기본적으로 **/P** 는 **SQLdiag** 실행 파일이 있는 폴더로 설정됩니다. 지원 폴더에는 XML 구성 파일, Transact-SQL 스크립트 및 진단 정보를 수집하는 동안 유틸리티에서 사용하는 기타 파일을 비롯한 **SQLdiag** 지원 파일이 있습니다. 이 옵션을 사용하여 대체 지원 파일 경로를 지정하면 **SQLdiag** 는 지정한 폴더에 없는 경우 필요한 지원 파일을 자동으로 복사합니다.  
  
> [!NOTE]  
>  현재 폴더를 지원 경로로 설정하려면 다음과 같이 명령줄에서 **%cd%** 를 지정합니다.  
>   
>  **SQLDIAG /P %cd%**  
  
 **/N** _output_folder_management_option_  
 **SQLdiag** 가 시작될 때 출력 폴더를 덮어쓸 것인지 또는 이름을 바꿀 것인지 설정합니다. 사용 가능한 옵션은 다음과 같습니다.  
  
 1 = 출력 폴더를 덮어씁니다(기본값).  
  
 2 = **SQLdiag** 가 시작될 때 출력 폴더의 이름을 SQLDIAG_00001, SQLDIAG_00002 등으로 바꿉니다. 현재 출력 폴더의 이름을 바꾼 다음 **SQLdiag** 는 기본 출력 폴더 SQLDIAG에 출력을 씁니다.  
  
> [!NOTE]  
>  **SQLdiag** 는 시작할 때 현재 출력 폴더에 출력을 추가하지 않습니다. 대신 기본 출력 폴더를 덮어쓰거나(옵션 1) 폴더의 이름을 바꾼 다음(옵션 2) SQLDIAG라는 새 기본 출력 폴더에 출력을 씁니다.  
  
 **/M** _machine1_ [ *machine2**machineN*] | *@machinelistfile*  
 구성 파일에 지정된 컴퓨터를 재정의합니다. 기본적으로 구성 파일은 SQLDiag.Xml이거나 **/I** 매개 변수를 사용하여 설정됩니다. 둘 이상의 컴퓨터를 지정할 경우 각 컴퓨터 이름을 공백으로 구분하십시오.  
  
 *@machinelistfile*을 사용하면 구성 파일에 저장할 컴퓨터 목록 파일 이름이 지정됩니다.  
  
 **/C** _file_compression_type_  
 **SQLdiag** 출력 폴더 파일에서 사용되는 파일 압축 유형을 설정합니다. 사용 가능한 옵션은 다음과 같습니다.  
  
 0 = 없음(기본값)  
  
 1 = NTFS 압축을 사용합니다.  
  
 **/B** [**+**]*start_time*  
 진단 데이터 수집 시작 날짜와 시간을 다음 형식으로 지정합니다.  
  
 YYYYMMDD_HH:MM:SS  
  
 시간은 24시간제 표시법으로 지정합니다. 예를 들어 오후 2시는 **14:00:00**으로 지정해야 합니다.  
  
 날짜 없이 HH:MM:SS에 **+** 를 사용하여 현재 날짜와 시간에 대한 상대 시간을 지정할 수 있습니다. 예를 들어 **/B +02:00:00**으로 지정하면 **SQLdiag** 에서는 2시간 후부터 정보 수집을 시작합니다.  
  
 **+** 와 지정한 *start_time*사이에 공백을 넣지 마세요.  
  
 지정한 시작 시간이 과거일 경우 **SQLdiag** 에서 강제로 시작 날짜를 변경하여 시작 날짜와 시간을 미래 시간으로 설정합니다. 예를 들어 현재 시간이 08:00:00인데 **/B 01:00:00** 으로 지정하면 **SQLdiag** 에서 강제로 시작 날짜를 다음 날로 변경합니다.  
  
 **SQLdiag** 는 유틸리티를 실행하는 컴퓨터의 현지 시간을 사용합니다.  
  
 **/E** [**+**]*stop_time*  
 진단 데이터 수집 종료 날짜와 시간을 다음 형식으로 지정합니다.  
  
 YYYYMMDD_HH:MM:SS  
  
 시간은 24시간제 표시법으로 지정합니다. 예를 들어 오후 2시는 **14:00:00**으로 지정해야 합니다.  
  
 날짜 없이 HH:MM:SS에 **+** 를 사용하여 현재 날짜와 시간에 대한 상대 시간을 지정할 수 있습니다. 예를 들어 시작 시간과 종료 시간을 **/B +02:00:00 /E +03:00:00**으로 지정하면 **SQLdiag** 에서는 2시간 후부터 정보 수집을 시작하고 3시간 동안 정보를 수집한 다음 중지하고 끝냅니다. **/B** 를 지정하지 않으면 **SQLdiag** 에서 즉시 진단 정보 수집을 시작하고 **/E**로 지정된 날짜와 시간에 종료합니다.  
  
 **+** 와 지정한 *start_time* 또는 *end_time*사이에 공백을 넣지 마세요.  
  
 **SQLdiag** 는 유틸리티를 실행하는 컴퓨터의 현지 시간을 사용합니다.  
  
 **/ A** _SQLdiag_application_name_  
 동일한 **인스턴스에 대해 여러** SQLdiag [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 유틸리티 인스턴스를 실행할 수 있도록 합니다.  
  
 각 *SQLdiag_application_name* 은 서로 다른 **SQLdiag**인스턴스를 식별합니다. *SQLdiag_application_name* 인스턴스와 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 이름은 전혀 관계가 없습니다.  
  
 *SQLdiag_application_name* 은 특정 **SQLdiag** 서비스 인스턴스를 시작하거나 중지하는 데 사용할 수 있습니다.  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 **SQLDIAG START /A** _SQLdiag_application_name_  
  
 또한 **/R** 옵션과 함께 사용하여 특정 **SQLdiag** 인스턴스를 서비스로 등록할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 **SQLDIAG /R /A** _SQLdiag_application_name_  
  
> [!NOTE]  
>  **SQLdiag** 는 *SQLdiag_application_name*에 대해 지정한 인스턴스 이름 앞에 DIAG$를 자동으로 붙입니다. **SQLdiag** 를 서비스로 등록하는 경우 이를 통해 구분이 가능한 서비스 이름이 제공됩니다.  
  
 /T { tcp [ ,*port* ] | np | lpc }  
 지정된 프로토콜을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
 tcp [,*port*]  
 TCP/IP(Transmission Control Protocol/Internet Protocol)입니다. 필요에 따라 연결을 위한 포트 번호를 지정할 수 있습니다.  
  
 np  
 명명된 파이프입니다. 기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 기본 인스턴스는 명명된 인스턴스에 대한 명명된 파이프 `\\.\pipe\sql\query` 및 `\\.\pipe\MSSQL$<instancename>\sql\query` 에서 수신합니다. 대체 파이프 이름을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결할 수는 없습니다.  
  
 lpc  
 로컬 프로시저 호출입니다. 이 공유 메모리 프로토콜은 클라이언트가 같은 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하는 경우 사용할 수 있습니다.  
  
 **/Q**  
 자동 모드에서 **SQLdiag** 를 실행합니다. **/Q** 는 암호 프롬프트와 같은 모든 프롬프트를 표시하지 않습니다.  
  
 **/G**  
 제네릭 모드에서 **SQLdiag** 를 실행합니다. **/G** 를 지정하면 시작 시 **SQLdiag** 에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결을 확인하거나 사용자가 **sysadmin** 고정 서버 역할의 멤버인지 확인하지 않습니다. 대신 **SQLdiag** 는 사용자에게 각각의 요청된 진단 정보를 수집할 수 있는 권한이 있는지 여부를 Windows를 통해 확인합니다.  
  
 **/G** 를 지정하지 않으면 **SQLdiag** 에서 사용자가 Windows **Administrators** 그룹의 멤버인지 확인하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Administrators **그룹 멤버가 아닐 경우** 진단 정보를 수집하지 않습니다.  
  
 **/R**  
 **SQLdiag** 를 서비스로 등록합니다. **SQLdiag** 를 서비스로 등록할 때 지정하는 모든 명령줄 인수는 나중에 서비스를 실행할 때 사용할 수 있도록 보관됩니다.  
  
 **SQLdiag** 를 서비스로 등록할 경우 기본 서비스 이름은 SQLDIAG입니다. **/A** 인수를 사용하여 서비스 이름을 변경할 수 있습니다.  
  
 다음과 같이 **START** 명령줄 인수를 사용하여 서비스를 시작할 수 있습니다.  
  
 **SQLDIAG START**  
  
 다음과 같이 **net start** 명령을 사용하여 서비스를 시작할 수도 있습니다.  
  
 **net 시작 SQLDIAG**  
  
 **/U**  
 서비스로 등록된 **SQLdiag** 의 등록을 취소합니다.  
  
 명명된 **SQLdiag** 인스턴스의 등록을 취소하는 경우에는 **/A** 인수도 사용합니다.  
  
 **/L**  
 각각 **/B** 또는 **/E** 인수를 사용하여 시작 시간이나 종료 시간도 지정한 경우 **SQLdiag** 가 연속 모드로 실행됩니다. 예약된 종료로 인해 진단 정보 수집이 중지되면**SQLdiag** 가 자동으로 다시 시작됩니다. 예를 들어 **/E** 또는 **/X** 인수를 사용하면 종료됩니다.  
  
> [!NOTE]  
>  **/B** 및 **/E** 명령줄 인수를 사용하여 시작 시간이나 종료 시간을 지정하지 않는 경우 **SQLdiag** 는 **/L** 인수를 무시합니다.  
  
 **/L** 은 서비스 모드를 나타내는 인수가 아닙니다. **SQLdiag** 를 서비스로 실행할 때 **/L** 을 사용하려면 해당 서비스를 등록할 때 명령줄에서 /L을 지정해야 합니다.  
  
 **/X**  
 스냅숏 모드에서 **SQLdiag** 를 실행합니다. **SQLdiag** 는 구성된 모든 진단 정보에 대해 스냅숏을 만들고 자동으로 종료됩니다.  
  
 **START** | **STOP** | **STOP_ABORT**  
 **SQLdiag** 서비스를 시작하거나 중지합니다. **STOP_ABORT** 는 현재 수행하고 있는 진단 정보 수집을 완료하지 않고 가능한 빨리 서비스를 강제 종료합니다.  
  
 이러한 서비스 제어 인수를 사용할 때는 명령줄에서 첫 번째 인수로 사용해야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 **SQLDIAG START**  
  
 명명된 **SQLdiag** 인스턴스를 지정하는 **/A**인수만 **START**, **STOP**또는 **STOP_ABORT** 와 함께 사용하여 특정 **SQLdiag** 서비스 인스턴스를 제어할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 **SQLDIAG START /A** _SQLdiag_application_name_  
  
## <a name="security-requirements"></a>보안 요구 사항  
  **SQLdiag** 명령줄 인수를 지정하여 일반 모드에서 **SQLdiag** 를 실행하지 않을 경우 **SQLdiag** 를 실행하는 사용자는 Windows **Administrators** 그룹의 멤버이면서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **sysadmin** 고정 서버 역할의 멤버여야 합니다. 기본적으로 **SQLdiag** 에서는 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 연결하지만 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증도 지원합니다.  
  
## <a name="performance-considerations"></a>성능 고려 사항  
 **SQLdiag** 를 실행할 때 성능에 주는 영향은 수집하도록 구성한 진단 데이터의 종류에 따라 다릅니다. 예를 들어 **추적 정보를 수집하도록** SQLdiag [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 를 구성한 경우 추적할 이벤트 클래스를 많이 선택할수록 서버 성능에 더 많은 영향을 줍니다.  
  
 **SQLdiag** 를 실행할 때 성능에 주는 영향은 구성한 진단 정보를 개별적으로 수집할 때 드는 노력을 모두 합한 것과 거의 같습니다. 예를 들어 **SQLdiag** 로 추적 정보를 수집할 경우 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]를 사용하여 해당 정보를 수집할 때와 성능에 주는 영향이 같습니다. **SQLdiag** 사용으로 인해 성능에 주는 영향은 매우 적습니다.  
  
## <a name="required-disk-space"></a>필요한 디스크 공간  
 **SQLdiag** 에서는 여러 가지 진단 정보를 수집할 수 있으므로 **SQLdiag** 를 실행하는 데 필요한 디스크 여유 공간은 그에 따라 다릅니다. 수집하는 진단 정보의 양은 서버에서 처리하는 작업의 성격과 양에 따라 다르며 몇 MB부터 몇 GB에 이르기까지 매우 다양합니다.  
  
## <a name="configuration-files"></a>구성 파일  
 시작 시 **SQLdiag** 에서는 지정된 구성 파일 및 명령줄 인수를 읽습니다. 사용자는 구성 파일에 **SQLdiag** 가 구성 파일에 수집할 진단 정보 유형을 지정합니다. 기본적으로 **SQLdiag** 에서는 SQLDiag.Xml 구성 파일을 사용합니다. 이 구성 파일은 해당 도구가 실행될 때마다 추출되며 **SQLdiag** 유틸리티 시작 폴더에 있습니다. 이 구성 파일은 XML 스키마인 SQLDiag_schema.xsd를 사용하며 이 스키마 또한 **SQLdiag** 를 실행할 때마다 실행 파일에서 유틸리티 시작 디렉터리로 추출됩니다.  
  
### <a name="editing-the-configuration-files"></a>구성 파일 편집  
 SQLDiag.Xml을 복사 및 편집하여 **SQLdiag** 에서 수집하는 진단 데이터의 유형을 변경할 수 있습니다. 구성 파일을 편집할 때는 항상 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]와 같은 XML 스키마에 대해 구성 파일의 유효성을 검사할 수 있는 XML 편집기를 사용하십시오. 직접 SQLDiag.Xml을 편집해서는 안 됩니다. 대신 SQLDiag.Xml을 복사하고 새 파일 이름으로 바꿔 같은 폴더에 저장합니다. 그런 다음 새 파일을 편집하고 **/I** 인수를 사용하여 **SQLdiag**에 전달합니다.  
  
#### <a name="editing-the-configuration-file-when-sqldiag-runs-as-a-service"></a>SQLdiag를 서비스로 실행할 때 구성 파일 편집  
 이미 **SQLdiag** 를 서비스로 실행한 경우 구성 파일을 편집하려면 **/U** 명령줄 인수를 지정하여 SQLDIAG 서비스의 등록을 취소한 다음 **/R** 명령줄 인수를 사용하여 이 서비스를 다시 등록합니다. 서비스의 등록을 취소하고 다시 등록하면 Windows 레지스트리에 캐시된 이전 구성 정보가 제거됩니다.  
  
## <a name="output-folder"></a>출력 폴더  
 **/O** 인수를 사용하여 출력 폴더를 지정하지 않으면 **SQLdiag** 가 **SQLdiag** 시작 폴더에 SQLDIAG라는 하위 폴더를 만듭니다. [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 와 같이 추적 정보의 양이 많은 진단 정보를 수집하는 경우 로컬 드라이브의 출력 폴더에 요청된 진단 정보 출력을 저장할 수 있는 충분한 공간이 있는지 확인합니다.  
  
 **SQLdiag** 를 다시 시작하면 출력 폴더의 내용을 덮어씁니다. 이 문제를 방지하려면 명령줄에서 **/N 2** 를 지정합니다.  
  
## <a name="data-collection-process"></a>데이터 수집 프로세스  
 **SQLdiag** 가 시작되면 SQLDiag.Xml에 지정된 진단 데이터를 수집하는 데 필요한 초기화 검사가 수행됩니다. 이 프로세스는 몇 초 정도 걸릴 수 있습니다. **SQLdiag** 를 콘솔 응용 프로그램으로 실행하는 경우 진단 데이터 수집을 시작하면 **SQLdiag** 에서 수집을 시작했으며 Ctrl+C를 눌러 중지할 수 있음을 알리는 메시지가 표시됩니다. **SQLdiag** 를 서비스로 실행하는 경우 이와 비슷한 메시지가 Windows 이벤트 로그에 기록됩니다.  
  
 **SQLdiag** 를 사용하여 재현할 수 있는 문제를 진단하는 경우 이 메시지가 표시된 다음에 서버에서 해당 문제를 재현해야 합니다.  
  
 **SQLdiag** 에서는 대부분의 진단 데이터를 병렬로 수집합니다. Windows 성능 로그 및 이벤트 로그에서 정보를 수집하는 경우를 제외하고 모든 진단 정보는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **sqlcmd** 유틸리티나 Windows 명령 처리기와 같은 도구에 연결하여 수집합니다. **SQLdiag** 에서는 컴퓨터당 작업자 스레드를 하나씩 사용하여 이러한 도구의 진단 데이터 수집을 모니터링하므로 동시에 여러 도구가 완료되기까지 기다려야 하는 경우도 있습니다. 수집이 진행되는 동안 **SQLdiag** 는 각 진단의 출력을 출력 폴더로 라우팅합니다.  
  
## <a name="stopping-data-collection"></a>데이터 수집 중지  
 **SQLdiag** 에서 진단 데이터를 수집하기 시작하면 사용자가 직접 중지하거나 지정한 시간에 중지되도록 구성한 경우를 제외하고 계속해서 데이터를 수집합니다. **/E** 인수를 사용하여 중지 시간을 지정하거나 **/X** 인수를 사용하여 **SQLdiag** 를 스냅숏 모드로 실행하면 지정한 시간에 중지되도록 **SQLdiag** 를 구성할 수 있습니다.  
  
 **SQLdiag** 가 중지되면 시작했던 모든 진단이 중지됩니다. 예를 들어 수집 중인 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 추적이 중지되고 실행 중인 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트 실행이 중지되며 데이터를 수집하는 동안 발생한 모든 하위 프로세스가 중지됩니다. 진단 데이터 수집이 완료되면 **SQLdiag** 가 종료됩니다.  
  
> [!NOTE]  
>  **SQLdiag** 서비스를 일시 중지하는 작업은 지원되지 않습니다. **SQLdiag** 서비스를 일시 중지하면 일시 중지했을 때 수집하던 진단 정보의 수집을 완료한 다음 중지됩니다. **SQLdiag** 를 중지한 다음 다시 시작하면 응용 프로그램이 다시 시작되며 출력 폴더가 덮어쓰여집니다. 출력 폴더를 덮어쓰지 않으려면 명령줄에서 **/N 2** 를 지정합니다.  
  
 **콘솔 응용 프로그램으로 실행하는 SQLdiag를 중지하려면**  
  
 **SQLdiag** 를 콘솔 응용 프로그램으로 실행하는 경우 **SQLdiag** 가 실행 중인 콘솔 창에서 Ctrl+C를 눌러 중지할 수 있습니다. Ctrl+C를 누르면 **SQLdiag** 데이터 수집이 종료되며 프로세스가 종료될 때까지 몇 분 정도 기다려야 한다는 메시지가 콘솔 창에 표시됩니다.  
  
 Ctrl+C를 두 번 눌러 모든 자식 진단 프로세스를 종료하고 즉시 애플리케이션을 종료합니다.  
  
 **서비스로 실행하는 SQLdiag를 중지하려면**  
  
 **SQLdiag** 를 서비스로 실행하는 경우 **SQLdiag** 시작 폴더에서 **SQLDiag STOP** 을 실행하여 중지합니다.  
  
 동일한 컴퓨터에서 여러 **SQLdiag** 인스턴스를 실행하는 경우 서비스를 중지할 때 명령줄에서 **SQLdiag** 인스턴스 이름을 전달할 수도 있습니다. 예를 들어 Instance1이라는 **SQLdiag** 인스턴스를 중지하려면 다음 구문을 사용합니다.  
  
```  
SQLDIAG STOP /A Instance1  
```  
  
> [!NOTE]  
>  **/A** 는 **START**, **STOP**또는 **STOP_ABORT**와 함께 사용할 수 있는 유일한 명령줄 인수입니다. 서비스 제어 동사 중 하나로 명명된 **SQLdiag** 인스턴스를 지정해야 하는 경우 이전 구문 예에서와 같이 명령줄에서 제어 동사 뒤에 **/A** 를 지정합니다. 제어 동사를 사용할 때는 명령줄에서 첫 번째 인수로 사용해야 합니다.  
  
 최대한 빨리 서비스를 중지하려면 유틸리티 시작 폴더에서 **SQLDIAG STOP_ABORT** 를 실행합니다. 이 명령을 사용하면 현재 수행 중인 진단 정보 수집이 완료되기를 기다리지 않고 중단합니다.  
  
> [!NOTE]  
>  **SQLDiag STOP** 또는 **SQLDIAG STOP_ABORT** 를 사용하여 **SQLdiag** 서비스를 중지할 수 있습니다. **SQLdiag** 또는 기타 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스를 중지할 때는 Windows 서비스 콘솔을 사용하지 마세요.  
  
## <a name="automatically-starting-and-stopping-sqldiag"></a>SQLdiag 자동 시작 및 중지  
 지정한 시간에 진단 데이터 수집을 자동으로 시작하고 중지하려면 24시간제 표시법을 사용하여 **/B**_start_time_ 및 **/E**_stop_time_ 인수를 사용합니다. 예를 들어 계속해서 02:00:00 경에 나타나는 문제를 해결하려면 01:00:00에 자동으로 진단 데이터 수집을 시작하여 03:00:00에 자동으로 중지하도록 **SQLdiag** 를 구성할 수 있습니다. 시작 시간과 중지 시간은 각각 **/B** 및 **/E** 인수를 사용하여 지정합니다. 24시간제 표시법을 사용하여 정확한 시작 및 중지 날짜와 시간을 YYYYMMDD_HH:MM:SS 형식으로 지정합니다. 현재를 기준으로 상대적인 시작 시간이나 중지 시간을 지정하려면 다음 예에서와 같이 시작 및 중지 시간 앞에 **+** 를 붙이고 날짜 부분(YYYYMMDD_)을 생략합니다. 그러면 **SQLdiag** 는 1시간 후부터 정보 수집을 시작하여 3시간 동안 정보를 수집한 다음 중지하고 종료합니다.  
  
```  
sqldiag /B +01:00:00 /E +03:00:00  
```  
  
 상대적인 *start_time* 을 지정하면 현재 날짜와 시간에 대한 상대 시간에 **SQLdiag** 가 시작됩니다. 상대적인 *end_time* 을 지정하면 지정한 **start_time** 에 대한 상대 시간에 *SQLdiag*가 종료됩니다. 지정한 시작 및 종료 날짜와 시간이 과거인 경우 **SQLdiag** 에서 시작 날짜와 시간이 미래가 되도록 시작 날짜를 강제로 변경합니다.  
  
 이는 선택하는 시작 및 종료 날짜에 중요한 영향을 줍니다. 다음 예를 살펴 보십시오.  
  
```  
sqldiag /B +01:00:00 /E 08:30:00  
```  
  
 현재 시간이 08:00일 경우 실제로 진단 정보 수집을 시작하기 전에 종료 시간이 지났습니다. 이러한 경우 **SQLdiag** 에서 자동으로 시작 및 종료 날짜를 다음 날로 조정하기 때문에 이 예에서 진단 정보 수집은 오늘 09:00에 시작되어( **+** 를 사용하여 상대 시작 시간 지정) 다음날 아침 08:30까지 계속됩니다.  
  
### <a name="stopping-and-restarting-sqldiag-to-collect-daily-diagnostics"></a>일일 진단 정보를 수집하는 SQLdiag 중지 및 다시 시작  
 수동으로 **SQLdiag**를 시작하고 중지할 필요 없이 지정한 진단 정보를 매일 수집하려면 **/L** 인수를 사용합니다. **/L** 인수를 사용하면 예약된 종료 후에 자동으로 다시 시작하여 **SQLdiag** 가 계속해서 실행됩니다. **/L** 을 지정한 경우 **SQLdiag** 가 **/E** 인수로 지정한 종료 시간에 도달해서 중지되거나 **/X** 인수를 사용하여 스냅숏 모드에서 실행되고 있기 때문에 중지되면 **SQLdiag** 가 종료되는 대신 다시 시작됩니다.  
  
 다음 예에서는 연속 모드에서 **SQLdiag** 를 실행하여 03:00:00부터 05:00:00까지 진단 데이터를 수집한 후 자동으로 다시 시작하도록 지정합니다.  
  
```  
sqldiag /B 03:00:00 /E 05:00:00 /L  
```  
  
 다음 예에서는 연속 모드에서 **SQLdiag** 를 실행하여 03:00:00에 진단 데이터 스냅숏을 만든 후 자동으로 다시 시작하도록 지정합니다.  
  
```  
sqldiag /B 03:00:00 /X /L  
```  
  
## <a name="running-sqldiag-as-a-service"></a>SQLdiag를 서비스로 실행  
 **SQLdiag** 를 사용하여 장시간 진단 데이터를 수집하면서 **SQLdiag** 를 실행 중인 컴퓨터에서 로그아웃해야 할 수도 있는 경우 이를 서비스로 실행할 수 있습니다.  
  
 **SQLDiag를 등록하여 서비스로 실행하려면**  
  
 명령줄에서 **/R** 인수를 지정하여 **SQLdiag** 를 등록하고 서비스로 실행할 수 있습니다. 그러면 **SQLDiag** 가 서비스로 실행되도록 등록됩니다. **SQLdiag** 서비스 이름은 SQLDIAG입니다. **SQLdiag** 를 서비스로 등록할 때 명령줄에서 지정한 다른 모든 인수는 보관되어 서비스를 시작할 때 다시 사용됩니다.  
  
 기본 SQLDIAG 서비스 이름을 변경하려면 **/A** 명령줄 인수를 사용하여 다른 이름을 지정합니다. **SQLdiag** 는 **/A** 를 사용하여 지정한 모든 **SQLdiag** 인스턴스 이름 앞에 DIAG$를 자동으로 붙여 구분이 가능한 서비스 이름을 만듭니다.  
  
 **SQLDIAG 서비스의 등록을 취소하려면**  
  
 서비스의 등록을 취소하려면 **/U** 인수를 지정합니다. 서비스로 등록된 **SQLdiag** 의 등록을 취소하면 서비스의 Windows 레지스트리 키도 삭제됩니다.  
  
 **SQLDIAG 서비스를 시작하거나 다시 시작하려면**  
  
 SQLDIAG 서비스를 시작하거나 다시 시작하려면 명령줄에서 **SQLDiag START** 를 실행합니다.  
  
 **/A** 인수를 사용하여 여러 **SQLdiag** 인스턴스를 실행하는 경우 서비스를 시작할 때 명령줄에서 **SQLdiag** 인스턴스 이름을 전달할 수도 있습니다. 예를 들어 Instance1이라는 **SQLdiag** 인스턴스를 시작하려면 다음 구문을 사용합니다.  
  
```  
SQLDIAG START /A Instance1  
```  
  
 **net start** 명령을 사용하여 SQLDIAG 서비스를 시작할 수도 있습니다.  
  
 **SQLdiag**를 다시 시작하면 현재 출력 폴더의 내용을 덮어씁니다. 이러한 문제를 방지하려면 명령줄에서 **/N 2** 를 지정하여 유틸리티가 시작될 때 출력 폴더의 이름을 바꿉니다.  
  
 **SQLdiag** 서비스를 일시 중지하는 작업은 지원되지 않습니다.  
  
## <a name="running-multiple-instances-of-sqldiag"></a>여러 SQLdiag 인스턴스 실행  
 명령줄에서 **/A** SQLdiag_application_name **을 지정하여 동일한 컴퓨터에서 여러**_SQLdiag_ 인스턴스를 실행할 수 있습니다. 이는 동일한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 동시에 다른 진단 정보 집합을 수집하는 데 유용합니다. 예를 들어 지속적으로 간단한 데이터 수집을 수행하도록 명명된 **SQLdiag** 인스턴스를 구성할 수 있습니다. 그런 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 특정 문제가 발생하는 경우 기본 **SQLdiag** 인스턴스를 실행하여 해당 문제에 대한 진단 정보를 수집하거나 [!INCLUDE[msCoName](../includes/msconame-md.md)] 고객 지원 서비스에서 수집을 요청한 진단 정보 집합을 수집하여 문제를 진단할 수 있습니다.  
  
## <a name="collecting-diagnostic-data-from-clustered-sql-server-instances"></a>클러스터형 SQL Server 인스턴스에서 진단 데이터 수집  
 **SQLdiag** 에서는 클러스터형 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 진단 데이터를 수집할 수 있습니다. 클러스터형 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 진단 정보를 수집하려면 SQLDiag.Xml 구성 파일에서 **\<Machine>** 요소의 **name** 특성에 대해 **"."** 를 지정해야 하며 명령줄에서 **/G** 인수를 지정하면 안 됩니다. 기본적으로 구성 파일에서 **name** 특성에는 **"."** 가 지정되고 **/G** 인수는 해제되어 있습니다. 일반적으로 클러스터형 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 정보를 수집할 때는 구성 파일을 편집하거나 명령줄 인수를 변경할 필요가 없습니다.  
  
 **"."** 를 컴퓨터 이름으로 지정하면 **SQLdiag** 에서는 컴퓨터가 클러스터에서 실행 중임을 감지하고 해당 클러스터에 설치된 모든 가상 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 동시에 진단 정보를 검색합니다. 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가상 인스턴스 중 하나에서만 진단 정보를 수집하려면 SQLDiag.Xml에서 **\<Machine>** 요소의 **name** 특성에 해당 가상 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]을 지정합니다.  
  
> [!NOTE]  
>  클러스터형 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 인스턴스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 추적 정보를 수집하려면 클러스터에서 관리 공유(ADMIN$)를 설정해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [명령 프롬프트 유틸리티 참조&#40;데이터베이스 엔진#41;](command-prompt-utility-reference-database-engine.md)  
  
  
