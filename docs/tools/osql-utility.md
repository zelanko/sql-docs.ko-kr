---
title: "osql 유틸리티 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: osql
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- operating systems [SQL Server], commands
- osql utility [SQL Server]
- stored procedures [SQL Server], command prompt
- scripts [SQL Server], command prompt
- RESET command
- GO command
- command prompt utilities [SQL Server], osql
- CTRL+C command
ms.assetid: cf530d9e-0609-4528-8975-ab8e08e40b9a
caps.latest.revision: "49"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 13a41dd247105dcce2580027c014aa266df5ed9c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="osql-utility"></a>osql 유틸리티
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]**osql** 유틸리티 입력할 수 있습니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일입니다. 이 유틸리티에서는 ODBC를 사용하여 서버와 통신합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이후 버전에서는 이 기능이 제거됩니다. 향후 개발 작업에서는 이 기능을 사용하지 않도록 하고 현재 이 기능을 사용하는 응용 프로그램은 수정하십시오. 대신 **sqlcmd** 을 사용합니다. 자세한 내용은 [sqlcmd Utility](../tools/sqlcmd-utility.md)을(를) 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
osql  
[-?] |  
[-L] |  
[  
  {  
     {-Ulogin_id [-Ppassword]} | –E }  
     [-Sserver_name[\instance_name]] [-Hwksta_name] [-ddb_name]  
     [-ltime_out] [-ttime_out] [-hheaders]  
     [-scol_separator] [-wcolumn_width] [-apacket_size]  
     [-e] [-I] [-D data_source_name]  
     [-ccmd_end] [-q "query"] [-Q"query"]  
     [-n] [-merror_level] [-r {0 | 1}]  
     [-iinput_file] [-ooutput_file] [-p]  
     [-b] [-u] [-R] [-O]  
]  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 **osql** 스위치의 구문 요약 정보를 표시합니다.  
  
 **-L**  
 로컬로 구성된 서버와 네트워크상에서 브로드캐스팅하는 서버의 이름을 표시합니다.  
  
> [!NOTE]  
>  네트워크에서 브로드캐스팅의 특성으로 인해 **osql** 은 모든 서버로부터 때맞춰 응답을 받지 못할 수 있습니다. 그러므로 반환되는 서버 목록은 이 옵션을 호출할 때마다 다를 수 있습니다.  
  
 **-U** *login_id*  
 사용자 로그인 ID입니다. 로그인 ID는 대/소문자를 구분합니다.  
  
 **-P** *password*  
 사용자가 지정하는 암호입니다. **-P** 옵션을 사용하지 않으면 **osql** 은 암호를 묻는 메시지를 표시합니다. 암호를 입력하지 않고 명령 프롬프트의 마지막에 **-P** 옵션을 사용하면 **osql** 은 기본 암호인 NULL을 사용합니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 자세한 내용은 [Strong Passwords](../relational-databases/security/strong-passwords.md)을 참조하세요.  
  
 암호는 대소문자를 구분합니다.  
  
 OSQLPASSWORD 환경 변수를 사용하면 현재 세션에 대한 기본 암호를 설정할 수 있습니다. 따라서 배치 파일에 암호를 하드 코딩할 필요가 없습니다.  
  
 **-P** 옵션으로 암호를 지정하지 않으면 **osql** 은 먼저 OSQLPASSWORD 변수를 검사합니다. 값을 설정하지 않으면 **osql** 은 기본 암호인 NULL을 사용합니다. 다음 예에서는 명령 프롬프트에서 OSQLPASSWORD 변수를 설정하고 **osql** 유틸리티에 액세스합니다.  
  
```  
C:\>SET OSQLPASSWORD=abracadabra  
C:\>osql   
```  
  
> [!IMPORTANT]  
>  암호를 마스킹하려면 **-U** 옵션과 함께 **-P** 옵션을 지정하지 마세요. 대신 **-U** 옵션 및 기타 스위치와 함께 **osql** 을 지정한 후 **-P**를 지정하지 말고 Enter 키를 누릅니다. 그러면 **osql** 이 암호를 묻는 메시지를 표시합니다. 이 방법을 사용하면 암호 입력 시 암호가 마스킹됩니다.  
  
 **-E**  
 암호를 요구하지 않고 트러스트된 연결을 사용합니다.  
  
 **-S** *server_name*[ **\\***instance_name*]  
 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 인스턴스를 지정합니다. 해당 서버 컴퓨터에 있는 기본 *인스턴스에 연결하려면* server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 을 지정합니다. 해당 서버에 있는 명명된 *인스턴스에 연결하려면***\\***server_name* instance_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 을 지정합니다. 서버를 지정하지 않으면 **osql** 은 로컬 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 기본 인스턴스에 연결됩니다. 네트워크의 원격 컴퓨터에서 **osql** 을 실행할 때 이 옵션이 필요합니다.  
  
 **-H** *wksta_name*  
 워크스테이션 이름입니다. 워크스테이션 이름은 **sysprocesses.hostname** 에 저장되고 **sp_who**에 의해 표시됩니다. 이 옵션을 지정하지 않으면 현재 컴퓨터 이름이 사용됩니다.  
  
 **-d** *db_name*  
 *osql* 을 시작할 때 USE **db_name**문을 실행합니다.  
  
 **-l** *time_out*  
 **osql** 로그인 제한 시간(초)을 지정합니다. 기본 **osql** 로그인 제한 시간은 8초입니다.  
  
 **-t** *time_out*  
 명령 제한 시간(초)을 지정합니다. *time_out* 값을 지정하지 않으면 명령이 무기한 실행됩니다.  
  
 **-h** *headers*  
 열 머리글 사이에 출력할 행의 수를 지정합니다. 기본적으로 각 쿼리 결과 집합마다 머리글을 한 번 출력합니다. 머리글을 출력하지 않으려면 -1을 사용합니다. -1을 사용하는 경우는**-h -1**이 아니라 **-h-1**과 같이 매개 변수와 설정 사이에 공백이 없어야 합니다.  
  
 **-s** *col_separator*  
 열 구분 기호 문자를 지정합니다. 기본값은 공백입니다. 운영 체제에서 특별한 의미를 갖는 문자(예: | ; & < >)를 사용하려면 해당 문자를 큰따옴표(")로 묶습니다.  
  
 **-w** *column_width*  
 출력에 사용할 화면의 너비를 설정할 수 있습니다. 기본값은 80자입니다. 출력 줄이 최대 화면 너비에 도달하면 여러 줄로 나뉘어집니다.  
  
 **-a** *packet_size*  
 다른 크기의 패킷을 요청할 수 있습니다. 유효한 *packet_size* 값은 512에서 65535까지입니다. 기본값 **osql** 은 서버 기본값입니다. 패킷 크기를 늘리면 GO 명령 사이에 SQL 문이 많은 크기가 큰 스크립트를 실행할 때 성능이 향상됩니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 의 테스트 결과에 의하면 일반적으로 8192를 설정했을 때 대량 복사 작업이 가장 빨리 수행됩니다. 더 큰 패킷 크기를 요청할 수 있지만 요청한 크기를 허용하지 않으면 **osql** 이 서버 기본값을 사용합니다.  
  
 **-e**  
 입력을 에코합니다.  
  
 **-I**  
 QUOTED_IDENTIFIER 연결 옵션을 설정합니다.  
  
 **-D** *data_source_name*  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]용 ODBC 드라이버를 사용하여 정의한 ODBC 데이터 원본에 연결합니다. **osql** 연결은 데이터 원본에 지정한 옵션을 사용합니다.  
  
> [!NOTE]  
>  다른 드라이버에서 정의한 데이터 원본에서는 이 옵션이 적용되지 않습니다.  
  
 **-c** *cmd_end*  
 명령 종료 문자를 지정합니다. 기본적으로 줄에 GO만 단독으로 입력하면 명령이 종료되어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 보내집니다. 명령 종료 문자를 다시 설정할 때는 앞에 백슬래시를 지정하는지 여부에 상관없이 [!INCLUDE[tsql](../includes/tsql-md.md)] 예약어 또는 운영 체제와 연관된 특별한 의미를 가진 문자를 사용하지 마십시오.  
  
 **-q "** *query* **"**  
 **osql** 이 시작될 때 쿼리를 실행하지만 쿼리가 완료되더라도 **osql** 을 끝내지 않습니다. 쿼리 문에는 GO를 포함할 수 없습니다. 일괄 처리에서 쿼리를 실행하면 %변수 또는 환경 %변수%를 사용할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SET table=sys.objects  
osql -E -q "select name, object_id from %table%"  
```  
  
 쿼리는 큰따옴표로 묶고 쿼리 안에 포함되는 모든 것은 작은따옴표로 묶습니다.  
  
 **-Q"** *query* **"**  
 쿼리를 실행하고 바로 **osql**을 끝냅니다. 쿼리는 큰따옴표로 묶고 쿼리 안에 포함되는 모든 것은 작은따옴표로 묶습니다.  
  
 **-n**  
 입력 줄에서 번호 및 프롬프트 기호(>)를 제거합니다.  
  
 **-m** *error_level*  
 오류 메시지 표시를 사용자 지정합니다. 지정한 심각도 이상의 오류에 대한 메시지 번호, 상태 및 오류 수준이 표시됩니다. 지정한 수준보다 낮은 심각도의 오류에 대해서는 표시되지 않습니다. **-1** 을 사용하여 모든 머리글을 메시지(정보 메시지도 포함)와 함께 반환합니다. **-1**을 사용하는 경우에는**-m -1**이 아니라 **-m-1**과 같이 매개 변수와 설정 사이에 공백이 없어야 합니다.  
  
 **-r** { **0**| **1**}  
 메시지 출력을 화면으로 리디렉션합니다(**stderr**). 매개 변수를 지정하지 않거나 **0**을 지정하면 심각도가 11 이상인 오류 메시지만 리디렉션됩니다. **1**을 지정하면 "print"를 포함하는 모든 메시지 출력이 리디렉션됩니다.  
  
 **-i** *input_file*  
 SQL 문 또는 저장 프로시저의 일괄 처리가 포함된 파일을 나타냅니다. **\<**-i **대신 보다 작음(**) 비교 연산자를 사용할 수 있습니다.  
  
 **-o** *output_file*  
 **osql**에서 출력을 받는 파일을 나타냅니다. **>**-o **대신 보다 큼(**) 비교 연산자를 사용할 수 있습니다.  
  
 *input_file* 이 유니코드가 아니고 **-u** 가 지정되지 않은 경우 *output_file* 이 OEM 형식으로 지정됩니다. *input_file* 이 유니코드이거나 **-u** 가 지정된 경우에는 *output_file* 이 유니코드 형식으로 지정됩니다.  
  
 **-p**  
 성능 통계를 출력합니다.  
  
 **-b**  
 오류가 발생하면 **osql** 을 끝내고 DOS ERRORLEVEL 값을 반환하도록 지정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 오류 메시지의 심각도가 11 이상이면 DOS ERRORLEVEL 변수에 1을 반환하고 아니면 0을 반환합니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] MS-DOS 배치 파일은 DOS ERRORLEVEL 값을 검사하여 오류를 적절하게 처리할 수 있습니다.  
  
 **-u**  
 *input_file* 형식에 관계없이 *output_file*이 유니코드 형식으로 저장되도록 지정합니다.  
  
 **-R**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC 드라이버가 통화, 날짜 및 시간 데이터를 문자 데이터로 변환할 때 클라이언트 설정을 사용하도록 지정합니다.  
  
 **-O**  
 이전 버전의 **osql** 동작과 일치하도록 특정 **isql**기능을 비활성화합니다. 다음 기능이 비활성화됩니다.  
  
-   EOF 일괄 처리  
  
-   콘솔 너비 자동 조정  
  
-   와이드 메시지  
  
 DOS ERRORLEVEL의 기본값을 -1로 설정합니다.  
  
> [!NOTE]  
>  위에 나열된 대/소문자를 구분하는 옵션을 사용하여 **-n**에서는 **-O** , **-D** 및 **osql**의 이후 버전에서는 이 기능이 제거됩니다.  
  
## <a name="remarks"></a>주의  
 위에 나열된 대/소문자를 구분하는 옵션을 사용하여 **osql** 유틸리티를 운영 체제에서 직접 시작할 수 있습니다. **osql**을 시작하면 osql이 SQL 문을 받아서 대화형으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 보냅니다. 결과는 서식 지정되어 화면에 표시됩니다(**stdout**). **osql**을 끝내려면 QUIT 또는 EXIT를 사용합니다.  
  
 **osql**을 시작할 때 사용자 이름을 지정하지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 환경 변수를 검사한 후 사용합니다. 예를 들어 **osqluser=(***user***)** 또는 **osqlserver=(***server***)**를 사용합니다. 환경 변수를 설정하지 않으면 워크스테이션 사용자 이름이 사용됩니다. 서버를 지정하지 않으면 워크스테이션 이름이 사용됩니다.  
  
 **-U** 또는 **-P** 옵션을 사용하지 않으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 인증 모드를 사용하여 연결을 시도합니다. 인증은 [!INCLUDE[msCoName](../includes/msconame-md.md)] osql **을 실행하는 사용자의**Windows 계정에 기반합니다.  
  
 **osql** 유틸리티는 ODBC API를 사용합니다. 이 유틸리티는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ISO 연결 옵션의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC 드라이버 기본 설정을 사용합니다. 자세한 내용은 ANSI 옵션 효과를 참조하십시오.  
  
> [!NOTE]  
>  **osql** 유틸리티는 CLR 사용자 정의 데이터 형식을 지원하지 않습니다. 이 데이터 형식을 처리하려면 **sqlcmd** 유틸리티를 사용해야 합니다. 자세한 내용은 [sqlcmd Utility](../tools/sqlcmd-utility.md)을(를) 참조하십시오.  
  
## <a name="osql-commands"></a>OSQL 명령  
 [!INCLUDE[tsql](../includes/tsql-md.md)] osql **내에서**문 외에도 다음 명령을 사용할 수 있습니다.  
  
|Command|Description|  
|-------------|-----------------|  
|GO|마지막 GO 이후에 입력한 모든 문을 실행합니다.|  
|RESET|입력한 모든 문을 지웁니다.|  
|QUIT 또는 EXIT( )|**osql**을 끝냅니다.|  
|CTRL+C|**osql**을 끝내지 않고 쿼리를 끝냅니다.|  
  
> [!NOTE]  
>  !! 및 ED 명령은 **osql**에서 더 이상 지원되지 않습니다.  
  
 명령 종료 문자인 GO(기본 문자), RESET EXIT, QUIT 및 Ctrl+C는 **osql** 프롬프트 바로 뒤의 줄 시작 부분에 나올 때만 인식합니다.  
  
 GO는 일괄 처리의 끝을 알려 주고 캐시된 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행하도록 신호를 보냅니다. 각 입력 줄의 끝에서 Enter 키를 누르면 **osql** 이 해당 줄의 문을 캐시합니다. GO를 입력한 다음 Enter 키를 누르면 현재 캐시된 모든 문을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 일괄 처리로 보냅니다.  
  
 현재 **osql** 유틸리티는 스크립트 끝에 GO가 있는 것으로 간주하므로 스크립트의 모든 문이 실행됩니다.  
  
 명령 종료 문자로 시작하는 줄을 입력하여 명령을 끝내십시오. 명령 종료 문자 다음에 정수를 써서 명령 실행 횟수를 지정할 수 있습니다. 예를 들어 다음 명령을 100번 실행하려면 다음을 입력하십시오.  
  
```  
SELECT x = 1  
GO 100  
```  
  
 결과는 실행이 끝날 때 한 번만 출력됩니다. **osql** 을 사용하면 각 줄에서 최대 1,000자까지 사용할 수 있습니다. 긴 문은 여러 줄로 나뉘어집니다.  
  
 Windows의 명령 재호출 기능을 사용하면 **osql** 문을 다시 호출하고 수정할 수 있습니다. RESET을 입력하면 기존 쿼리 버퍼를 지울 수 있습니다.  
  
 **osql** 은 저장 프로시저를 실행할 때 일괄 처리의 각 결과 집합 사이에 빈 줄을 출력합니다. 또한, 실행되는 문에 적용되지 않을 때는 "적용된 행 없음" 메시지가 나타나지 않습니다.  
  
## <a name="using-osql-interactively"></a>osql을 대화형으로 사용  
 **osql** 을 대화형으로 사용하려면 명령 프롬프트에서 **osql** 명령 및 옵션을 입력합니다.  
  
 다음과 같은 명령을 입력하면 Stores.qry 파일과 같이 **osql** 실행 쿼리가 들어 있는 파일을 읽어올 수 있습니다.  
  
```  
osql -E -i stores.qry  
```  
  
 다음과 같은 명령을 입력하면 쿼리가 들어 있는 Titles.qry 파일을 읽어 들이고 그 결과를 다른 파일에 보낼 수 있습니다.  
  
```  
osql -E -i titles.qry -o titles.res  
```  
  
> [!IMPORTANT]  
>  가능하면 **-E**옵션(신뢰할 수 있는 연결)을 사용합니다.  
  
 **osql** 을 대화형으로 사용하면 **:r***file_name*을 지정하여 운영 체제 파일을 명령 버퍼로 읽을 수 있습니다. 그러면 *file_name* 의 SQL 스크립트가 직접 서버에 한 번의 일괄 처리로 보내집니다.  
  
> [!NOTE]  
>  **osql**을 사용할 때 일괄 처리 구분 기호 GO가 SQL 스크립트 파일에 나타나면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 이를 구문 오류로 처리합니다.  
  
## <a name="inserting-comments"></a>주석 삽입  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] osql **을 사용하여**에 전송하는 Transact-SQL 문에 주석을 포함할 수 있습니다. 허용되는 두 가지 주석 유형은 -- 및 /*...\*/입니다.  
  
## <a name="using-exit-to-return-results-in-osql"></a>EXIT를 사용하여 osql의 결과 반환  
 SELECT 문의 결과를 **osql**의 반환 값으로 사용할 수 있습니다. 숫자일 경우 마지막 결과 행의 마지막 열은 4바이트 정수(long)로 변환됩니다. MS-DOS는 하위 바이트를 부모 프로세스 또는 운영 체제 오류 수준에 전달합니다. Windows에서는 4바이트 정수 전체를 전달합니다. 구문은 다음과 같습니다.  
  
```  
EXIT ( < query > )  
```  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
EXIT(SELECT @@ROWCOUNT)  
```  
  
 EXIT 매개 변수를 배치 파일의 일부로 포함할 수도 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
osql -E -Q "EXIT(SELECT COUNT(*) FROM '%1')"  
```  
  
 **osql** 유틸리티는 괄호 **()** 안에 입력된 모든 내용을 그대로 서버에 전달합니다. 저장 시스템 프로시저가 설정을 선택하고 값을 반환하면 선택 내용만 반환합니다. EXIT**()** 문의 괄호 사이에 아무 것도 없으면 이 문 앞에 나오는 모든 문을 실행한 다음 값을 반환하지 않고 종료합니다.  
  
 다음과 같은 4개의 EXIT 형식이 있습니다.  
  
-   EXIT  
  
> [!NOTE]  
>  일괄 처리를 실행하지 않고 즉시 종료하며 값을 반환하지 않습니다.  
  
-   EXIT**()**  
  
> [!NOTE]  
>  일괄 처리를 실행한 다음 종료하며 값을 반환하지 않습니다.  
  
-   EXIT**(***query***)**  
  
> [!NOTE]  
>  쿼리를 포함한 일괄 처리를 실행하며 쿼리 결과를 반환한 다음 종료합니다.  
  
-   상태가 127인 RAISERROR  
  
> [!NOTE]  
>  **osql** 스크립트에 RAISERROR를 사용할 때 상태 127이 발생하면 **osql** 이 종료되고 메시지 ID가 클라이언트에 반환됩니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
RAISERROR(50001, 10, 127)  
```  
  
 이 오류가 발생하면 **osql** 스크립트가 종료되고 메시지 ID 50001이 클라이언트에 반환됩니다.  
  
 -1부터 -99까지의 반환 값은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 예약되어 있습니다. **osql** 에는 다음과 같은 값이 정의되어 있습니다.  
  
-   -100  
  
     반환 값을 선택하기 전에 오류가 발생했습니다.  
  
-   -101  
  
     반환 값을 선택할 때 행을 찾을 수 없습니다.  
  
-   -102  
  
     반환 값을 선택할 때 변환 오류가 발생했습니다.  
  
## <a name="displaying-money-and-smallmoney-data-types"></a>money 및 smallmoney 데이터 형식 표시  
 **는 내부적으로 네 개의 소수 자릿수로 값을 저장하지만** osql **은 두 개의 소수 자릿수로** money **및** smallmoney [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 형식을 표시합니다. 예를 들어, 다음과 같습니다.  
  
```  
SELECT CAST(CAST(10.3496 AS money) AS decimal(6, 4))  
GO  
```  
  
 이 문의 결과는 `10.3496`로 표시됩니다. 모든 소수 자릿수를 그대로 사용하여 값이 저장되었습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [설명&#40;MDX&#41;](../mdx/comment-mdx.md)   
 [-&#40; 설명 &#41; &#40; Mdx&#41;](../mdx/comment-mdx-operator-reference.md)   
 [CAST 및 convert&#40; Transact SQL &#41;](../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Raiserror&#40; Transact SQL &#41;](../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
