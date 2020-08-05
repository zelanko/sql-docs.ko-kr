---
title: 프로파일러 유틸리티
description: 프로파일러 유틸리티는 SQL Server Profiler 도구를 시작합니다. 옵션 인수를 사용하여 애플리케이션 시작 방법을 제어할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], profiler90 utility
- profiler90 utility
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: e91c30a9-0d29-4f84-bcb8-e8fb62afadda
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a6a51b6949d3b387c1284bdd5cbaa9a64b3cfa37
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917074"
---
# <a name="profiler-utility"></a>프로파일러 유틸리티
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
  **profiler** 유틸리티는 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 도구를 실행합니다. 이 항목에서 나중에 나열된 옵션 인수를 사용하여 애플리케이션 시작 방법을 제어할 수 있습니다.  
  
> [!NOTE]  
>  **profiler** 유틸리티는 추적 스크립팅을 위한 유틸리티가 아닙니다. 자세한 내용은 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
profiler  
    [ /? ] |  
[  
{  
{ /U login_id [ /P password ] }  
| /E  
}  
{[ /S sql_server_name ] | [ /A analysis_services_server_name ] }  
[ /D database ]  
[ /T "template_name" ]  
[ /B { "trace_table_name" } ]  
{ [/F "filename" ] | [ /O "filename" ] }  
[ /L locale_ID ]  
[ /M "MM-DD-YY hh:mm:ss" ]  
[ /R ]  
[ /Z file_size ]  
]  
```  
  
## <a name="arguments"></a>인수  
 **/?**  
 **profiler** 인수의 구문 요약 정보를 표시합니다.  
  
 **/U** *login_id*  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 위한 사용자 로그인 ID입니다. 로그인 ID는 대/소문자를 구분합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]입니다.  
  
 **/P** *password*  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 위한 암호를 지정합니다. 사용자가 원하는 대로 지정할 수 있습니다.  
  
 **/E**  
 현재 사용자의 자격 증명으로 Windows 인증을 사용하는 연결을 지정합니다.  
  
 **/S**  *sql_server_name*  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스를 지정합니다. 프로파일러는 지정된 **/U** 및 **/P** 스위치 또는 **/E** 스위치에서 지정된 인증 정보를 사용하여 지정된 서버에 자동으로 연결합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 명명된 인스턴스에 연결하려면 **/S** *sql_server_name*\\*instance_name*을 사용합니다.  
  
 **/A**  *analysis_services_server_name*  
 Analysis Services 인스턴스를 지정합니다. 프로파일러는 지정된 **/U** 및 **/P** 스위치 또는 **/E** 스위치에서 지정된 인증 정보를 사용하여 지정된 서버에 자동으로 연결합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 명명된 인스턴스에 연결하려면 **/A** *analysis_services_server_name\instance_name*을 사용합니다.  
  
 **/D** *database*  
 연결에 사용할 데이터베이스 이름을 지정합니다. 데이터베이스를 지정하지 않으면 이 옵션은 지정된 사용자의 기본 데이터베이스를 선택합니다.  
  
 **/B "** *trace_table_name* **"**  
 프로파일러를 시작할 때 로드할 추적 테이블을 지정합니다. 데이터베이스, 사용자나 스키마 및 테이블을 지정해야 합니다.  
  
 **/T"** *template_name* **"**  
 추적을 구성하기 위해 로드할 템플릿을 지정합니다. 템플릿 이름을 따옴표로 묶어야 합니다. 또한 템플릿 이름은 시스템 템플릿 디렉터리나 사용자 템플릿 디렉터리에 있어야 합니다. 두 디렉터리에 이름이 같은 템플릿 두 개가 있을 경우 시스템 디렉터리의 템플릿이 로드됩니다. 지정한 이름의 템플릿이 없을 경우 표준 템플릿이 로드됩니다. *template_name*에 템플릿의 파일 확장명(.tdf)을 포함하지 마세요. 다음은 그 예입니다.  
  
```  
/T "standard"  
```  
  
 **/F"** *filename* **"**  
 프로파일러를 시작할 때 로드할 추적 파일의 경로와 이름을 지정합니다. 전체 경로 및 파일 이름은 따옴표로 묶어야 합니다. 이 옵션은 **/O**와 함께 사용할 수 없습니다.  
  
 **/O "** *filename*  **"**  
 추적 결과를 기록할 파일의 경로와 이름을 지정합니다. 전체 경로 및 파일 이름은 따옴표로 묶어야 합니다. 이 옵션은 **/F**와 함께 사용할 수 없습니다.  
  
 **/L** *locale_ID*  
 사용할 수 없습니다.  
  
 **/M "** *MM-DD-YY hh:mm:ss* **"**  
 추적을 중지할 날짜와 시간을 지정합니다. 중지 시간을 따옴표로 묶어야 합니다. 아래 표의 매개 변수에 따라 중지 시간을 지정합니다.  
  
|매개 변수|정의|  
|---------------|----------------|  
|MM|두 자릿수 월|  
|DD|두 자릿수 일|  
|YY|두 자릿수 연도|  
|hh|24시간제의 두 자릿수 시간|  
|MM|두 자릿수 분|  
|ss|두 자릿수 초|  
  
> [!NOTE]  
>  **에서** 날짜 및 시간 값 표시에 국가별 설정 사용 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]옵션이 설정되어 있는 경우 "MM-DD-YY hh:mm:ss" 형식만 사용할 수 있습니다. 이 옵션이 설정되어 있지 않은 경우 "YYYY-MM-DD hh:mm:ss" 날짜 및 시간 형식을 사용해야 합니다.  
  
 **/R**  
 추적 파일 롤오버를 사용합니다.  
  
 **/Z**  *file_size*  
 추적 파일 크기(MB)를 지정합니다. 기본 크기는 5MB입니다. 롤오버를 사용하는 경우 모든 롤오버 파일이 이 인수에서 지정한 값으로 제한됩니다.  
  
## <a name="remarks"></a>설명  
 특정 템플릿을 사용하여 추적을 시작하려면 **/S** 와 **/T** 옵션을 함께 사용합니다. 예를 들어 MyServer\MyInstance에 있는 Standard 템플릿을 사용하여 추적을 시작하려면 명령 프롬프트에서 다음을 입력합니다.  
  
```  
profiler /S MyServer\MyInstance /T "Standard"  
```  
  
## <a name="see-also"></a>참고 항목  
 [명령 프롬프트 유틸리티 참조&#40;데이터베이스 엔진#41;](../tools/command-prompt-utility-reference-database-engine.md)  
  
  
