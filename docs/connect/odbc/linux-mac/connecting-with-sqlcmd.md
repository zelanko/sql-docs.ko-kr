---
title: sqlcmd를 사용하여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a782db89033da42ebf17ed33565ec680fafa0d04
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68005916"
---
# <a name="connecting-with-sqlcmd"></a>sqlcmd를 사용하여 연결
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[sqlcmd](https://go.microsoft.com/fwlink/?LinkID=154481) 유틸리티는 Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver에서 사용할 수 있습니다.
  
다음 명령은 Windows 인증(Kerberos) 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 각각 사용하는 방법을 보여 줍니다.
  
```  
sqlcmd -E -Sxxx.xxx.xxx.xxx  
sqlcmd -Sxxx.xxx.xxx.xxx -Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>사용 가능한 옵션

현재 릴리스에서 다음 옵션을 사용할 수 있습니다.  
  
- -? `sqlcmd` 사용을 표시합니다.  
  
- -a 패킷 크기를 요청합니다.  
  
- -b 오류가 발생하는 경우 배치 작업을 종료합니다.  
  
- -c *batch_terminator* 일괄 처리 종결자를 지정합니다.  
  
- -C 서버 인증서를 신뢰합니다.  

- -d *database_name* `sqlcmd`를 시작할 때 USE `USE` *database_name* 문을 실행합니다.  

- -D `sqlcmd` -S 옵션에 전달된 값이 DSN(데이터 원본 이름)으로 해석되도록 합니다. 자세한 내용은 이 항목의 끝에 있는 "`sqlcmd` 및 `bcp`에서 DSN 지원"을 참조하세요.  
  
- -e 표준 출력 디바이스(stdout)에 입력 스크립트를 기록합니다.

- -E 신뢰할 수 있는 연결을 사용합니다(통합된 인증). Linux 또는 macOS 클라이언트에서 통합된 인증을 사용하는 신뢰할 수 있는 연결을 만드는 방법에 대한 자세한 내용은 [통합 인증 사용](../../../connect/odbc/linux-mac/using-integrated-authentication.md)을 참조하세요.

- -h *number_of_rows* 열 머리글 사이에 출력할 행의 수를 지정합니다.  
  
- -H 워크스테이션 이름을 지정합니다.  
  
- -i *input_file*[,*input_file*[,...]] SQL 문 또는 저장 프로시저의 일괄 처리가 포함된 파일을 식별합니다.  
  
- -I `SET QUOTED_IDENTIFIER` 연결 옵션을 ON으로 설정합니다.  
  
- -k 제어 문자를 제거하거나 바꿉니다.  
  
- **-K**_application\_intent_  
서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 현재 **ReadOnly**값만 지원됩니다. **-K** 를 지정하지 않으면 `sqlcmd`가 AlwaysOn 가용성 그룹에 있는 보조 복제본에 연결할 수 없습니다. 자세한 내용은 [ODBC Driver on Linux and macOS - High Availability and Disaster Recovery](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)(Linux 및 macOS의 ODBC 드라이버 - 고가용성, 재해 복구)를 참조하세요.  
  
> [!NOTE]  
> **-K** 가 CTP for SUSE Linux에서 지원되지 않습니다. 그러나 `sqlcmd`에 전달된 DSN 파일에서 **ApplicationIntent=ReadOnly** 키워드를 지정합니다. 자세한 내용은 이 항목의 끝에 있는 "`sqlcmd` 및 `bcp`에서 DSN 지원"을 참조하세요.  
  
- -l *timeout* 서버에 연결을 시도할 때 `sqlcmd` 로그인 제한 시간(초)을 지정합니다.

- -m *error_level* stdout에 보낼 오류 메시지를 제어합니다.  
  
- **-M**_multisubnet\_failover_  
[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 가용성 그룹 또는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **-M**을 지정합니다. **-M**은 현재 활성 상태인 서버에 대한 장애 조치를 빠르게 검색하고 연결할 수 있도록 지원합니다. **–M**이 지정되지 않으면 **-M** 이 해제되어 있습니다. [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]에 대한 자세한 내용은 [Linux 및 macOS의 ODBC 드라이버 - 고가용성 및 재해 복구](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)를 참조하세요.  
  
> [!NOTE]  
> **-M** 이 CTP for SUSE Linux에서 지원되지 않습니다. 그러나 `sqlcmd`에 전달된 DSN 파일에서 **MultiSubnetFailover=Yes** 키워드를 지정합니다. 자세한 내용은 이 항목의 끝에 있는 "`sqlcmd` 및 `bcp`에서 DSN 지원"을 참조하세요.  
  
- -N 연결을 암호화합니다.  
  
- -o *output_file*`sqlcmd`에서 출력을 받는 파일을 식별합니다.  
  
- -p 모든 결과 집합에 대한 성능 통계를 출력합니다.  
  
- -P 사용자 암호를 지정합니다.  
  
- -q *commandline_query* `sqlcmd`가 시작될 때 쿼리를 실행하지만 쿼리 실행이 완료되더라도 종료하지 않습니다.  

- -Q *commandline_query* `sqlcmd`가 시작될 때 쿼리를 실행합니다. 쿼리가 완료되면 `sqlcmd`가 종료됩니다.  

- -r 오류 메시지를 stderr로 리디렉션합니다.

- -R 드라이버에서 클라이언트의 국가별 설정을 사용하여 통화, 날짜/시간 데이터를 문자 데이터로 변환하도록 합니다. 현재 en_US(미국 영어) 서식만 사용합니다.
  
- -s *column_separator_char* 열 구분 기호를 지정합니다.  

- -S [*protocol*:] *server*[ **,** _port_]  
연결할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정하거나 -D가 사용된 경우 DSN을 지정합니다. Linux 및 macOS 기반 ODBC 드라이버에는 -S가 필요합니다. **tcp**만 유효한 프로토콜입니다.  
  
- -t *query_timeout* 명령(또는 SQL 문)이 시간 초과까지의 시간(초)을 지정합니다.  
  
- -u input_file 형식에 관계없이 output_file이 유니코드 형식으로 저장되도록 지정합니다.  
  
- -U *login_id* 사용자 로그인 ID를 지정합니다.  
  
- -V *error_severity_level* ERRORLEVEL 변수를 설정하는 데 사용되는 심각도를 제어합니다.  
  
- -w *column_width* 출력할 화면 너비를 지정합니다.  
  
- -W 열에서 후행 공백을 제거합니다.  
  
- -x 변수 대체를 사용하지 않습니다.  
  
- -X 명령, 시작 스크립트 및 환경 변수를 사용하지 않습니다.  
  
- -y *variable_length_type_display_width* `sqlcmd` 스크립팅 변수 `SQLCMDMAXFIXEDTYPEWIDTH`를 설정합니다.
  
- -Y *fixed_length_type_display_width* `sqlcmd` 스크립팅 변수 `SQLCMDMAXVARTYPEWIDTH`를 설정합니다.


## <a name="available-commands"></a>사용할 수 있는 명령

현재 릴리스에서 다음 명령을 사용할 수 있습니다.  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>사용할 수 없는 옵션
현재 릴리스에서 다음 옵션을 사용할 수 없습니다.  

- -A DAC(관리자 전용 연결)를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 로그인합니다. DAC(관리자 전용 연결)를 만드는 방법에 대한 자세한 내용은 [Programming Guidelines](../../../connect/odbc/linux-mac/programming-guidelines.md)을 참조하세요.  
  
- -f *code_page* 입력 및 출력 코드 페이지를 지정합니다.  
  
- -L 로컬로 구성된 서버 컴퓨터와 네트워크상에서 브로드캐스팅하는 서버 컴퓨터의 이름을 나열합니다.  
  
- -v `sqlcmd` 스크립트에서 사용할 수 있는 `sqlcmd` 스크립팅 변수를 만듭니다.  
  
다음과 같은 대체 방법을 사용할 수 있습니다. 한 파일에 매개 변수를 저장하여 다른 파일에 추가할 수 있습니다. 그러면 매개 변수 파일을 사용하여 값을 바꿀 수 있습니다. 예를 들어 다음과 같은 내용으로 `a.sql`(매개 변수 파일)이라는 파일을 만듭니다.
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
그런 다음, 대체할 매개 변수를 사용하여 `b.sql`이라는 파일을 만듭니다.  
  
    select $(ColumnName) from $(TableName)  

명령줄에서 다음 명령을 사용하여 `a.sql` 및 `b.sql`을 `c.sql`로 결합합니다.  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
`sqlcmd`를 실행하고 `c.sql`을 입력 파일로 사용합니다.  
  
    slqcmd -S<...> -P<..> -U<..> -I c.sql  

- -z *password* 암호를 변경합니다.  
  
- -Z *password* 암호를 변경하고 종료합니다.  

## <a name="unavailable-commands"></a>사용할 수 없는 명령

현재 릴리스에서 다음 명령을 사용할 수 없습니다.  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>sqlcmd 및 bcp에서 DSN 지원

-D를 지정하는 경우 **sqlcmd** 또는 **bcp** `-S` 옵션(또는 **sqlcmd** :Connect 명령)의 서버 이름 대신 DSN(데이터 원본 이름)을 지정할 수 있습니다. -D는 **sqlcmd** 또는 **bcp**가 -S 옵션으로 DSN에 지정된 서버에 연결되게 합니다.  
  
시스템 DSN이 ODBC SysConfigDir 디렉터리의 `odbc.ini` 파일에 저장됩니다(표준 설치에서는`/etc/odbc.ini`). 사용자 DSN이 사용자 홈 디렉터리의 `.odbc.ini`(`~/.odbc.ini`)에 저장됩니다.
  
Linux 또는 macOS의 DSN에서 다음 항목이 지원됩니다.

-   **ApplicationIntent=ReadOnly**  

-   **Database=** _database\_name_  
  
-   **Driver=ODBC Driver 11 for SQL Server** 또는 **Driver=ODBC Driver 13 for SQL Server**
  
-   **MultiSubnetFailover=Yes**  
  
-   **Server=** _server\_name\_or\_IP\_address_  
  
-   **Trusted_Connection=yes**|**no**  
  
DSN에서는 DRIVER 항목만 필요하지만 서버에 연결하려면 `sqlcmd` 또는 `bcp`에서 SERVER 항목의 값이 필요합니다.  

동일한 옵션이 DSN 및 `sqlcmd` 또는 `bcp` 명령줄에서 지정된 경우 명령줄 옵션이 DSN에서 사용되는 값을 재정의합니다. 예를 들어 DSN에 DATABASE 항목이 있고 `sqlcmd` 명령줄이 **-d**를 포함하는 경우 **-d**에 전달된 값이 사용됩니다. **Trusted_Connection=yes**가 DSN에서 지정된 경우 Kerberos 인증이 사용되고 사용자 이름( **–U**) 및 암호( **–P**)(제공된 경우)가 무시됩니다.

다음 별칭을 정의하여 `isql`을 호출하는 기존 스크립트는 `sqlcmd`를 사용하도록 수정할 수 있습니다. `alias isql="sqlcmd -D"`  

## <a name="see-also"></a>참고 항목  
[**bcp**를 사용하여 연결](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
