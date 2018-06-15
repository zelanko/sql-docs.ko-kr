---
title: Sqlcmd를 사용 하 여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c330fd329f28fa7d89b62b9af6bb8d4bb67c2bc4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853088"
---
# <a name="connecting-with-sqlcmd"></a>sqlcmd를 사용하여 연결
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[sqlcmd](http://go.microsoft.com/fwlink/?LinkID=154481) 유틸리티는에서 사용할 수는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux와 macOS에서 합니다.
  
다음 명령은 Windows 인증 (Kerberos)을 사용 하는 방법을 보여 줍니다 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인증의 경우 각각:
  
```  
sqlcmd –E –Sxxx.xxx.xxx.xxx  
sqlcmd –Sxxx.xxx.xxx.xxx –Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>사용 가능한 옵션

현재 릴리스에서 다음 옵션을 사용할 수 있습니다.  
  
- -? 디스플레이 `sqlcmd` 사용 합니다.  
  
- -요청을 주고받을 때 패킷 크기입니다.  
  
- 오류가 있으면 Terminate 일괄 작업-b를 선택 합니다.  
  
- -c *batch_terminator* 일괄 처리 종결자를 지정 합니다.  
  
- -C 서버 인증서 신뢰 합니다.  

- -d *database_name* 문제는 `USE ` *database_name* 문을 시작할 때 `sqlcmd`합니다.  

- 차원으로 인해에 전달 된 값은 `sqlcmd` -S 옵션이 데이터 원본 이름 (DSN)으로 해석 되도록 합니다. 자세한 내용은 참조 하십시오. "에서 DSN 지원 `sqlcmd` 및 `bcp`"이이 항목의 끝에 있습니다.  
  
- -e 표준 출력 장치 (stdout)에 입력된 스크립트를 작성 합니다.

- -E 트러스트 된 연결 (통합된 인증)를 사용 합니다. Linux 또는 macOS 클라이언트에서 통합된 인증을 사용 하는 신뢰할 수 있는 연결을 만드는 방법에 대 한 자세한 내용은 참조 [통합 인증을 사용](../../../connect/odbc/linux-mac/using-integrated-authentication.md)합니다.

- -h *number_of_rows* 열 머리글 사이 출력할 행 수를 지정 합니다.  
  
- -H 워크스테이션 이름을 지정 합니다.  
  
- -i *input_file*[,*input_file*[,...]] 포함 된 SQL 문의 일괄 처리 또는 저장 프로시저 파일을 식별 합니다.  
  
- -I 집합은 `SET QUOTED_IDENTIFIER` 연결 옵션을 ON입니다.  
  
- -k 제거 하거나 제어 문자를 바꿉니다.  
  
- **-K * * * application_intent*  
서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 현재 **ReadOnly**값만 지원됩니다. 경우 **-K** 를 지정 하지 않으면 `sqlcmd` AlwaysOn 가용성 그룹에 보조 복제본에 대 한 연결을 지원 하지 않습니다. 자세한 내용은 참조 [macOS-고가용성 및 재해 복구 및 Linux 기반 ODBC 드라이버](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)합니다.  
  
> [!NOTE]  
> **-K** 가 CTP for SUSE Linux에서 지원되지 않습니다. 그러나을 지정할 수는 **ApplicationIntent = ReadOnly** 에 전달 된 DSN 파일에서 키워드 `sqlcmd`합니다. 자세한 내용은 참조 하십시오. "에서 DSN 지원 `sqlcmd` 및 `bcp`"이이 항목의 끝에 있습니다.  
  
- -l *timeout* 초 수를 지정는 `sqlcmd` 서버에 연결 하려고 할 때 로그인 제한 시간입니다.

- -m *error_level* 제어 stdout에는 오류 메시지를 보냅니다.  
  
- **-M * * * multisubnet_failover*  
[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 가용성 그룹 또는 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **-M**을 지정합니다. **-M** 보다 빠르게 검색 하 고 장애 조치 (현재) 활성 서버 연결을 제공 합니다. **–M** 이 지정되지 않으면 **-M** 이 해제되어 있습니다. 에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], 참조 [macOS-고가용성 및 재해 복구 및 Linux 기반 ODBC 드라이버](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)합니다.  
  
> [!NOTE]  
> **-M** 이 CTP for SUSE Linux에서 지원되지 않습니다. 그러나을 지정할 수는 **MultiSubnetFailover = Yes** 에 전달 된 DSN 파일에서 키워드 `sqlcmd`합니다. 자세한 내용은 참조 하십시오. "에서 DSN 지원 `sqlcmd` 및 `bcp`"이이 항목의 끝에 있습니다.  
  
- -N 연결을 암호화 합니다.  
  
- -o *output_file* 에서 출력을 받는 파일을 식별 `sqlcmd`합니다.  
  
- -p 모든 결과 집합에 대 한 성능 통계를 인쇄 합니다.  
  
- -P 사용자 암호를 지정 합니다.  
  
- -q *commandline_query* 쿼리를 실행할 때 `sqlcmd` 시작 되지만 쿼리 실행이 완료 된 경우에 종료 하지 않습니다.  

- -Q *commandline_query* 쿼리를 실행할 때 `sqlcmd` 시작 합니다. `sqlcmd` 쿼리가 완료 될 때 종료 됩니다.  

- -r 리디렉션 오류 메시지를 stderr입니다.

- -R 하면 드라이버가 통화, 날짜 및 시간 데이터를 문자 데이터로 변환 하려면 클라이언트의 국가별 설정을 사용 하도록 합니다. 현재 en_US(미국 영어) 서식만 사용합니다.
  
- -s *column_separator_char* 열 구분 기호 문자를 지정 합니다.  

- -S [*프로토콜*:] *서버*[**, * * * 포트*]  
인스턴스를 지정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 연결할 또는-D는 경우를 사용 하는 DSN입니다. Linux와 macOS에서 ODBC 드라이버-S. 필요 **tcp** 유일 하 게 유효한 프로토콜입니다.  
  
- -t *query_timeout* 명령 (또는 SQL 문) 시간 초과 되기 전의 시간 (초) 수를 지정 합니다.  
  
- -u 지정 해당 output_file input_file 형식에 관계 없이 유니코드 형식으로 저장 됩니다.  
  
- -U *login_id* 사용자 로그인 ID를 지정 합니다.  
  
- -V *error_severity_level* ERRORLEVEL 변수를 설정 하는 데 사용 되는 심각도 제어 합니다.  
  
- -w *column_width* 출력에 사용할 화면의 너비를 지정 합니다.  
  
- -W 열에서 후행 공백을 제거 합니다.  
  
- 변수 대체-x 비활성화 합니다.  
  
- -X 명령, 시작 스크립트 및 환경 변수를 사용 하지 않도록 설정 합니다.  
  
- -y *variable_length_type_display_width* 설정는 `sqlcmd` 스크립팅 변수 `SQLCMDMAXFIXEDTYPEWIDTH`합니다.
  
- -Y *fixed_length_type_display_width* 설정는 `sqlcmd` 스크립팅 변수 `SQLCMDMAXVARTYPEWIDTH`합니다.


## <a name="available-commands"></a>사용 가능한 명령

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
현재 릴리스에서 다음 옵션은 사용할 수 없습니다.  

- -A가에 로그인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 관리자 전용된 연결 (DAC). 관리자 전용된 연결 (DAC)을 확인 하는 방법에 대 한 정보를 참조 하십시오. [프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)합니다.  
  
- -f *code_page* 입력 및 출력 코드 페이지를 지정 합니다.  
  
- -L 로컬로 구성 된 서버 컴퓨터와 네트워크상에서 브로드캐스팅하는 서버 컴퓨터의 이름을 나열 합니다.  
  
- -v 만들기는 `sqlcmd` 에 사용할 수 있는 스크립팅 변수는 `sqlcmd` 스크립트입니다.  
  
다음과 같은 대체 방법을 사용할 수 있습니다: 다른 파일에 추가할 수 있습니다는 하나의 파일 안에 매개 변수를 넣습니다. 그러면 매개 변수 파일을 사용하여 값을 바꿀 수 있습니다. 예를 들어 파일을 만들 `a.sql` (매개 변수 파일) 다음 내용을 사용 하 여:
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
다음 파일을 만들 `b.sql`, 대체에 대 한 매개 변수를 사용 합니다.  
  
    select $(ColumnName) from $(TableName)  

명령줄에서 결합 `a.sql` 및 `b.sql` 에 `c.sql` 다음 명령을 사용 하 여:  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
실행 `sqlcmd` 사용 하 여 `c.sql` 입력 파일로:  
  
    slqcmd -S<…> -P<..> –U<..> -I c.sql  

- -z *암호* 암호를 변경 합니다.  
  
- -Z *암호* 암호 변경 후 종료 합니다.  

## <a name="unavailable-commands"></a>사용할 수 없는 명령

현재 릴리스에서 다음 명령을 사용할 수 있습니다.  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>sqlcmd 및 bcp에서 DSN 지원

데이터 원본 이름 (DSN) 대신에 서버 이름 지정할 수는 **sqlcmd** 또는 **bcp** `-S` 옵션 (또는 **sqlcmd** : Connect 명령)-4. 지정 하는 경우 -D **sqlcmd** 또는 **bcp** -S 옵션에 의해 DSN에서 지정 된 서버에 연결 합니다.  
  
시스템 Dsn에 저장 되는 `odbc.ini` ODBC SysConfigDir 디렉터리의 파일 (`/etc/odbc.ini` 표준 설치에서). 사용자 Dsn에 저장 된 `.odbc.ini` 사용자의 홈 디렉터리에서 (`~/.odbc.ini`).
  
Linux 또는 macOS DSN에는 다음 항목이 지원 됩니다.

-   **ApplicationIntent = ReadOnly**  

-   **데이터베이스 = * * * database_name*  
  
-   **드라이버 ODBC Driver 11 for SQL Server =** 또는 **드라이버 ODBC Driver 13 for SQL Server =**
  
-   **MultiSubnetFailover = Yes**  
  
-   **Server = * * * server_name_or_IP_address*  
  
-   **Trusted_Connection=yes**|**no**  
  
Dsn에서는 DRIVER 항목만 필요 하지만 서버에 연결 하는 데 `sqlcmd` 또는 `bcp` 서버 항목에는 값이 필요 합니다.  

동일한 옵션이 DSN에서 지정 된 경우와 `sqlcmd` 또는 `bcp` 명령줄에서 명령줄 옵션 DSN에서 사용 되는 값을 무시 합니다. 예를 들어 DSN에 DATABASE 항목이 고 `sqlcmd` 명령줄에는 포함 **-d**, 전달 되는 값 **-d** 사용 됩니다. 경우 **Trusted_Connection = yes** Kerberos 인증이 사용 되는 이름과 사용자 DSN에 지정 된 (**– U**) 및 암호 (**– P**)도 제공 하는 경우 무시 됩니다.

호출 하는 기존 스크립트 `isql` 사용 하도록 수정할 수 `sqlcmd` 다음 별칭을 정의 하 여: `alias isql="sqlcmd –D"`합니다.  

## <a name="see-also"></a>관련 항목:  
[사용 하 여 연결 **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
