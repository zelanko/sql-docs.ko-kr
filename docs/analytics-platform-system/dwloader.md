---
title: dwloader 명령줄 로더
description: dwloader는 테이블 행을 기존 테이블에 대량으로 로드 하는 PDW (병렬 데이터 웨어하우스) 명령줄 도구입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7dd0ccf960b53b3cd1b474f61c60a58ff9b0a2c6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767052"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 dwloader 명령줄 로더
**dwloader** 는 테이블 행을 기존 테이블에 대량으로 로드 하는 PDW (병렬 데이터 웨어하우스) 명령줄 도구입니다. 행을 로드할 때 모든 행을 테이블의 끝에 추가 (*추가 모드* 또는 *fastappend 모드*) 하거나, 새 행을 추가 하 고 기존 행을 업데이트 (*upsert 모드*) 하거나, 로드 하기 전에 기존 행을 모두 삭제 하 고 모든 행을 빈 테이블 (*다시 로드 모드*)에 삽입할 수 있습니다.  
  
**데이터 로드 프로세스**  
  
1.  원본 데이터를 준비합니다.  
  
    자체 ETL 프로세스를 사용 하 여 로드 하려는 원본 데이터를 만듭니다. 원본 데이터는 대상 테이블의 스키마와 일치 하도록 형식이 지정 되어야 합니다. 원본 데이터를 하나 이상의 텍스트 파일에 저장 하 고 텍스트 파일을 로드 하는 서버에서 동일한 디렉터리에 복사 합니다. 로드 서버에 대 한 자세한 내용은 [로드 서버 가져오기 및 구성](acquire-and-configure-loading-server.md) 을 참조 하세요.  
  
2.  로드 옵션을 준비 합니다.  
  
    사용할 로드 옵션을 결정 합니다. 로드 옵션을 구성 파일에 저장 합니다. 로드 서버의 로컬 위치에 구성 파일을 복사 합니다. **Dwloader** 구성 옵션은이 항목에 설명 되어 있습니다.  
  
3.  로드 오류 옵션을 준비 합니다.  
  
    **Dwloader** 에서 로드에 실패 한 행을 처리 하는 방법을 결정 합니다. 부하를 수행 하기 위해 **dwloader** 는 먼저 준비 테이블에 데이터를 로드 한 다음 대상 테이블로 데이터를 전송 합니다. 로더가 준비 테이블에 데이터를 로드할 때 로드에 실패 한 행의 수를 추적 합니다. 예를 들어, 형식이 올바르게 지정 되지 않은 행은 로드 되지 않습니다. 실패 한 행은 거부 파일에 복사 됩니다. 기본적으로 다른 거부 임계값을 지정 하지 않으면 첫 번째 거부 후에 부하가 중단 됩니다.  
  
4.  **Dwloader**를 설치 합니다.  
  
    아직 설치 되지 않은 경우 로드 서버에 dwloader를 설치 합니다. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  **Dwloader**를 실행 합니다.  
  
    로드 서버에 로그인 하 고 적절 한 명령줄 옵션을 사용 하 여 실행 파일 **dwloader.exe** 를 실행 합니다.  
  
6.  결과를 확인 합니다.  
  
    -R으로 지정 된 실패 한 행 파일을 확인 하 여 로드에 실패 한 행이 있는지 확인할 수 있습니다. 이 파일이 비어 있으면 모든 행이 성공적으로 로드 됩니다. **dwloader** 는 트랜잭션 이므로 모든 단계가 실패 한 경우 (거부 된 행 제외) 모든 단계는 초기 상태로 롤백됩니다.  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>구문  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]
    [ -l ]   
}  
```  
  
## <a name="arguments"></a>인수  
**-h**  
로더 사용에 대 한 간단한 도움말 정보를 표시 합니다. 다른 명령줄 매개 변수를 지정 하지 않은 경우에만 도움말이 표시 됩니다.  
  
**-U** *login_name*  
로드를 수행할 수 있는 적절 한 권한이 있는 유효한 SQL Server 인증 로그인입니다.  
  
**-P** *password*  
*Login_name*SQL Server 인증에 대 한 암호입니다.  
  
**-W**  
Windows 인증을 사용합니다. *Login_name* 또는 *암호가* 필요 하지 않습니다. 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
명령줄 매개 변수 대신 *parameter_file_name*매개 변수 파일을 사용 합니다. *parameter_file_name* 는 *user_name* 와 *암호*를 제외한 모든 명령줄 매개 변수를 포함할 수 있습니다. 명령줄과 매개 변수 파일에 매개 변수가 지정 된 경우 명령줄은 file 매개 변수를 재정의 합니다.  
  
매개 변수 파일에는 한 줄에 접두사 없이 하나의 매개 변수가 포함 되어 있습니다 **-** .  
  
예제:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S** *target_appliance*  
로드 된 데이터를 받을 SQL Server PDW 어플라이언스를 지정 합니다.  
  
*Infiniband 연결의*경우 *target_appliance* <어플라이언스-이름>-SQLCTL01로 지정 됩니다. 이 명명 된 연결을 구성 하려면 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)을 참조 하세요.  
  
이더넷 연결의 경우 *target_appliance* 는 제어 노드 클러스터에 대 한 IP 주소입니다.  
  
생략 하는 경우 dwloader는 dwloader가 설치 될 때 지정 된 값으로 기본 설정 됩니다. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [ *schema*].*table_name*  
대상 테이블의 세 부분으로 구성 된 이름입니다.  
  
**-I** *source_data_location*  
로드할 하나 이상의 소스 파일의 위치입니다. 각 원본 파일은 gzip으로 압축 된 텍스트 파일 또는 텍스트 파일 이어야 합니다. 각 gzip 파일에 하나의 원본 파일만 압축할 수 있습니다.  
  
원본 파일의 형식을 지정 하려면:  
  
-   로드 옵션에 따라 원본 파일의 형식을 지정 해야 합니다.  
  
-   원본 파일의 각 줄은 하나의 테이블 행에 대 한 데이터를 포함 합니다. 원본 데이터는 대상 테이블의 스키마와 일치 해야 합니다. 열 순서와 데이터 유형도 일치 해야 합니다. 행의 각 필드는 대상 테이블의 열을 나타냅니다.  
  
-   기본적으로 필드는 가변 길이 이며 구분 기호로 구분 됩니다. 구분 기호 유형을 지정 하려면 <variable_length_column_options> 명령줄 옵션을 사용 합니다. 고정 길이 필드를 지정 하려면 <fixed_width_column_options> 명령줄 옵션을 사용 합니다.  
  
원본 데이터 위치를 지정 하려면:  
  
-   원본 데이터 위치는 로드 하는 서버에 있는 디렉터리의 로컬 경로 또는 네트워크 경로일 수 있습니다.  
  
-   디렉터리의 모든 파일을 지정 하려면 디렉터리 경로와 * 와일드 카드 문자를 차례로 입력 합니다.  로더는 원본 데이터 위치에 있는 하위 디렉터리에서 파일을 로드 하지 않습니다. Gzip 파일에 디렉터리가 있는 경우 로더 오류가 발생 합니다.  
  
-   디렉터리에 일부 파일을 지정 하려면 문자와 * 와일드 카드를 조합 하 여 사용 합니다.  
  
명령 하나를 사용 하 여 여러 파일을 로드 하려면:  
  
-   모든 파일은 동일한 디렉터리에 있어야 합니다.  
  
-   파일은 모두 텍스트 파일, 모든 gzip 파일 또는 텍스트와 gzip 파일의 조합 이어야 합니다.  
  
-   모든 파일에는 헤더 정보가 포함 될 수 없습니다.  
  
-   모든 파일은 동일한 문자 인코딩 형식을 사용 해야 합니다. -E 옵션을 참조 하세요.  
  
-   모든 파일을 동일한 테이블에 로드 해야 합니다.  
  
-   모든 파일은 하나의 파일 처럼 연결 되 고 로드 되며 거부 된 행은 단일 거부 파일로 이동 합니다.  
  
예제:  
  
-   -i \\ \loadserver\loads\daily \\ *. release.tar.gz  
  
-   -i \\ \loadserver\loads\daily \\ * .txt  
  
-   -i \\ \loadserver\loads\daily\monday. *  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\ \loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
로드 오류가 발생 한 경우 **dwloader** 는 로드에 실패 한 행을 저장 하 고 오류는 *load_failure_file_name*이라는 파일에 오류 정보를 설명 합니다. 이 파일이 이미 있으면 dwloader는 기존 파일을 덮어씁니다. *load_failure_file_name* 는 첫 번째 오류가 발생할 때 생성 됩니다. 모든 행이 성공적으로 로드 되 면 *load_failure_file_name* 생성 되지 않습니다.  
  
**-fh** *number_header_rows*  
*Source_data_file_name*시작 부분에서 무시할 줄 (행) 수입니다. 기본값은 0입니다.  
  
<variable_length_column_options>  
문자 구분 가변 길이 열을 포함 하는 *source_data_file_name* 에 대 한 옵션입니다. 기본적으로 *source_data_file_name* 는 가변 길이 열에 ASCII 문자를 포함 합니다.  
  
ASCII 파일의 경우에는 구분 기호를 연속으로 배치 하 여 Null이 표시 됩니다. 예를 들어, 파이프로 구분 된 파일 ("|")에서 NULL은 "| |"로 표시 됩니다. 쉼표로 구분 된 파일에서 NULL은 ",,"로 표시 됩니다. 또한 **-E** (--emptyStringAsNull) 옵션을 지정 해야 합니다. -E에 대 한 자세한 내용은 아래를 참조 하세요.  
  
**-e** *character_encoding*  
데이터 파일에서 로드할 데이터의 문자 인코딩 형식을 지정 합니다. 옵션은 ASCII (기본값), UTF8, UTF16 또는 UTF16BE입니다. 여기서 UTF16은 little endian이 고 UTF16BE은 big endian입니다. 이러한 옵션은 대/소문자를 구분 하지 않습니다.  
  
**-t** *field_delimiter*  
행의 각 필드 (열)에 대 한 구분 기호입니다. 필드 구분 기호는 이러한 ASCII 이스케이프 문자 또는 ASCII 16 진수 값 중 하나 이상입니다.  
  
|Name|이스케이프 문자|16 진수 문자|  
|--------|--------------------|-----------------|  
|탭|\t|0x09|  
|CR (캐리지 리턴)|\r|0x0d|  
|줄 바꿈 (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|쉼표|','|0x2c|  
|큰따옴표|\\"|0x22|  
|작은따옴표|\\'|0x27|  
  
명령줄에서 파이프 문자를 지정 하려면 큰따옴표 ("|")로 묶습니다. 이렇게 하면 명령줄 파서에서 잘못 해석 하지 않습니다. 다른 문자는 작은따옴표로 묶여 있습니다.  
  
예제:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t ' ~ | ~ '  
  
**-r** *row_delimiter*  
원본 데이터 파일의 각 행에 대 한 구분 기호입니다. 행 구분 기호는 하나 이상의 ASCII 값입니다.  
  
CR (캐리지 리턴), 줄 바꿈 (LF) 또는 탭 문자를 구분 기호로 지정 하려면 이스케이프 문자 (\r, \n, \t) 또는 16 진수 값 (0x, 0d, 09)을 사용할 수 있습니다. 다른 특수 문자를 구분 기호로 지정 하려면 해당 16 진수 값을 사용 합니다.  
  
CR + LF의 예:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR의 예:  
  
-r \r  
  
-r 0x0d  
  
LF의 예:  
  
-r \n  
  
-r 0x0a  
  
Unix에는 LF가 필요 합니다. Windows에는 CR이 필요 합니다.  
  
**-s** *string_delimiter*  
텍스트 구분 입력 파일의 문자열 데이터 형식 필드에 대 한 구분 기호입니다. 문자열 구분 기호는 하나 이상의 ASCII 값입니다.  문자 (예:-s *) 또는 16 진수 값으로 지정할 수 있습니다 (예: 큰따옴표의 경우-s 0x22).  
  
예제:  
  
삭제  
  
-s 0x22  
  
< fixed_width_column_options>  
고정 길이 열을 포함 하는 원본 데이터 파일에 대 한 옵션입니다. 기본적으로 *source_data_file_name* 는 가변 길이 열에 ASCII 문자를 포함 합니다.  
  
-E가 UTF8 인 경우 고정 너비 열은 지원 되지 않습니다.  
  
**-w** *fixed_width_config_file*  
각 열의 문자 수를 지정 하는 구성 파일의 경로 및 이름입니다. 모든 필드를 지정 해야 합니다.  
  
이 파일은 로드 서버에 상주해 야 합니다. 경로는 UNC, 상대 또는 절대 경로일 수 있습니다. *Fixed_width_config_file* 의 각 줄은 한 열의 이름과 해당 열의 문자 수를 포함 합니다. 열 마다 다음과 같이 한 줄이 있고 파일의 순서는 대상 테이블의 순서와 일치 해야 합니다.  
  
*column_name* = *num_chars*  
  
*column_name* = *num_chars*  
  
고정 너비 구성 파일의 예:  
  
SalesCode = 3  
  
SalesID = 10  
  
*Source_data_file_name*의 예제 줄:  
  
230Shirts0056  
  
320Towels1356  
  
이전 예제에서 첫 번째 로드 된 행에는 SalesCode = ' 230 ' 및 Salescode = ' Shirts0056 '가 있습니다. 로드 된 두 번째 행에는 SalesCode = ' 320 ' 및 SaleID = ' Towels1356 '가 있습니다.  
  
고정 너비 모드에서 선행 및 후행 공백 또는 데이터 형식 변환을 처리 하는 방법에 대 한 자세한 내용은 [dwloader의 데이터 형식 변환 규칙](dwloader-data-type-conversion-rules.md)을 참조 하세요.  
  
**-e** *character_encoding*  
데이터 파일에서 로드할 데이터의 문자 인코딩 형식을 지정 합니다. 옵션은 ASCII (기본값), UTF8, UTF16 또는 UTF16BE입니다. 여기서 UTF16은 little endian이 고 UTF16BE은 big endian입니다. 이러한 옵션은 대/소문자를 구분 하지 않습니다.  
  
-E가 UTF8 인 경우 고정 너비 열은 지원 되지 않습니다.  
  
**-r** *row_delimiter*  
원본 데이터 파일의 각 행에 대 한 구분 기호입니다. 행 구분 기호는 하나 이상의 ASCII 값입니다.  
  
CR (캐리지 리턴), 줄 바꿈 (LF) 또는 탭 문자를 구분 기호로 지정 하려면 이스케이프 문자 (\r, \n, \t) 또는 16 진수 값 (0x, 0d, 09)을 사용할 수 있습니다. 다른 특수 문자를 구분 기호로 지정 하려면 해당 16 진수 값을 사용 합니다.  
  
CR + LF의 예:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR의 예:  
  
-r \r  
  
-r 0x0d  
  
LF의 예:  
  
-r \n  
  
-r 0x0a  
  
Unix에는 LF가 필요 합니다. Windows에는 CR이 필요 합니다.  
  
**-D** { **ymd** \| ydm \| mdy \| myd \| dmy \| dym \| *custom_date_format* }  
입력 파일의 모든 날짜/시간 필드에 대 한 월 (m), 일 (d) 및 연도 (y)의 순서를 지정 합니다. 기본 순서는 ymd입니다. 동일한 원본 파일에 대해 여러 주문 형식을 지정 하려면-dt 옵션을 사용 합니다.  
  
ymd \|  
ydm 및 amy는 동일한 입력 형식을 허용 합니다. 모두 날짜의 시작 또는 끝에 연도를 사용할 수 있습니다. 예를 들어 **ydm** 및 adate **dmy** 형식의 경우 입력 파일에 2013-02-03 또는 02-03-2013이 있을 수 있습니다.  
  
ydm  
Datetime 및 smalldatetime 데이터 형식의 열에는 ydm 형식의 입력만 로드할 수 있습니다. 데이터 형식의 datetime2, date 또는 datetimeoffset 열에 ydm 값을 로드할 수 없습니다.  
  
mdy  
mdy는 \<month> \<space> \<day> \<comma> \<year> 를 허용 합니다.  
  
1975 년 1 월 1 일에 대 한 mdy 입력 데이터의 예:  
  
-   1975 년 1 월 1 일  
  
-   01 년 1 월 1 일, 75  
  
-   1 월/1/75  
  
-   01011975  
  
myd  
2010 년 3 월 4 일에 대 한 입력 파일 예제: 03-2010-04, 3/2010/4  
  
dym  
3 월 4 일에 대 한 입력 파일 예제 2010:04-2010-03, 4/2010/3  
  
*custom_date_format*  
*custom_date_format* 은 사용자 지정 날짜 형식 (예: MM/dd/yyyy) 이며 이전 버전과의 호환성을 위해서만 포함 됩니다. dwloader는 사용자 지정 날짜 형식을 적용 하지 않습니다. 대신, 사용자 지정 날짜 형식을 지정 하는 경우 **dwloader** 는이를 ymd, ydm, mdy, myd, dym 또는 dmy의 해당 설정으로 변환 합니다.  
  
예를 들어-D MM/dd/yyyy를 지정 하는 경우 dwloader는 모든 날짜 입력이 month first, day, year (mdy)로 정렬 될 것으로 예상 합니다. 사용자 지정 날짜 형식으로 지정 된 두 개의 문자 월, 2 자리 날짜 및 4 자리 연도를 적용 하지 않습니다. 날짜 형식이-D MM/dd/yyyy: 01/02/2013, 02.2013, 1/2/2013 인 경우 입력 파일에서 날짜 형식을 지정할 수 있는 몇 가지 예는 다음과 같습니다.  
  
보다 포괄적인 서식 지정 정보는 [dwloader의 데이터 형식 변환 규칙](dwloader-data-type-conversion-rules.md)을 참조 하세요.  
  
**-dt** *datetime_format_file*  
각 datetime 형식은 *datetime_format_file*이라는 파일에 지정 됩니다. 명령줄 매개 변수와 달리 공백을 포함 하는 파일 매개 변수는 큰따옴표로 묶어야 합니다. 데이터를 로드할 때 datetime 형식을 변경할 수 없습니다. 원본 데이터 파일 및 대상 테이블의 해당 열은 동일한 형식 이어야 합니다.  
  
각 줄에는 대상 테이블의 열 이름과 해당 날짜/시간 형식이 포함 됩니다.  
  
예제:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
준비 테이블을 포함 하는 데이터베이스 이름입니다. 기본값은-T 옵션을 사용 하 여 지정 된 데이터베이스입니다 .이 데이터베이스는 대상 테이블의 데이터베이스입니다. 준비 데이터베이스를 사용 하는 방법에 대 한 자세한 내용은 [준비 데이터베이스 만들기](staging-database.md)를 참조 하세요.  
  
**-M** *load_mode_option*  
데이터를 추가, upsert 또는 다시 로드할지 여부를 지정 합니다. 기본 모드는 추가입니다.  
  
추가  
로더는 대상 테이블의 기존 행 끝에 행을 삽입 합니다.  
  
fastappend  
로더는 임시 테이블을 사용 하지 않고 행을 대상 테이블의 기존 행 끝에 직접 삽입 합니다. fastappend에는 다중 트랜잭션 (-m) 옵션이 필요 합니다. Fastappend를 사용 하는 경우 준비 데이터베이스를 지정할 수 없습니다. Fastappend를 사용 하는 롤백이 없습니다. 즉, 실패 하거나 중단 된 로드에서의 복구가 사용자의 부하 프로세스에 의해 처리 되어야 합니다.  
  
upsert **-K**  *merge_column* [,... *n* ]  
로더는 SQL Server Merge 문을 사용 하 여 기존 행을 업데이트 하 고 새 행을 삽입 합니다.  
  
-K 옵션은 병합의 기준이 될 열을 지정 합니다. 이러한 열은 고유 행을 나타내는 병합 키를 형성 합니다. 병합 키가 대상 테이블에 있으면 해당 행이 업데이트 됩니다. Merge 키가 대상 테이블에 없으면 해당 행이 추가 됩니다.  
  
해시 분산 테이블의 경우 병합 키는 배포 열을 포함 하거나 포함 해야 합니다.  
  
복제 된 테이블의 경우 병합 키는 하나 이상의 열을 조합한 것입니다. 이러한 열은 응용 프로그램의 요구 사항에 따라 지정 됩니다.  
  
여러 열을 공백 없이 쉼표로 구분 하거나 공백으로 구분 하 여 작은따옴표로 묶어야 합니다.  
  
원본 테이블의 두 행에 일치 하는 병합 키 값이 있는 경우 해당 행은 동일 해야 합니다.  
  
로딩  
로더는 원본 데이터를 삽입 하기 전에 대상 테이블을 자릅니다.  
  
**-b** *batchsize*  
Microsoft 지원에서 사용 하는 경우에만 사용 하는 것이 좋습니다 *.이는 DMS가 계산* 노드에서 SQL Server 인스턴스로 수행 하는 대량 복사의 SQL Server 일괄 처리 크기입니다.  *Batchsize* 를 지정 하면 SQL Server PDW는 각 부하에 대해 동적으로 계산 되는 일괄 처리 로드 크기를 재정의 합니다.  
  
SQL Server 2012 PDW부터 제어 노드는 기본적으로 각 로드에 대 한 일괄 처리 크기를 동적으로 계산 합니다. 이 자동 계산은 메모리 크기, 대상 테이블 형식, 대상 테이블 스키마, 로드 형식, 파일 크기 및 사용자의 리소스 클래스와 같은 여러 매개 변수를 기반으로 합니다.  
  
예를 들어 로드 모드가 FASTAPPEND이 고 테이블에 클러스터형 columnstore SQL Server PDW 인덱스가 있는 경우에는 기본적으로 일괄 처리 크기 1048576를 사용 하 여 행 그룹을 닫고 델타 저장소를 통하지 않고 columnstore에 직접 로드 하 게 됩니다. 메모리에서 1048576의 일괄 처리 크기를 허용 하지 않는 경우 dwloader는 더 작은 batchsize를 선택 합니다.  
  
로드 유형이 FASTAPPEND 이면 *batchsize* 가 테이블에 데이터를 로드 하는 데 적용 됩니다. 그렇지 않으면 *batchsize* 가 준비 테이블에 데이터를 로드 하는 데 적용 됩니다.  
  
<reject_options>  
로더에서 허용할 로드 실패 횟수를 결정 하는 옵션을 지정 합니다. 로드 실패가 임계값을 초과 하면 로더가 중단 되 고 행이 커밋되지 않습니다.  
  
**-rt** { **value** | 백분율}  
**-Rv** *reject_value* 옵션의-*reject_value* 행 수 (값) 또는 실패 비율 (백분율) 인지 여부를 지정 합니다. 기본값은 value입니다.  
  
백분율 옵션은-rs 옵션에 따라 간격으로 발생 하는 실시간 계산입니다.  
  
예를 들어 로더가 100 행을 로드 하려고 시도 하 고 25 fail 및 75이 성공 하면 실패율은 25%입니다.  
  
**-rv** *reject_value*  
로드를 중지 하기 전까지 허용 되는 행 거부의 수 또는 비율을 지정 합니다. **-Rt** 옵션은 *reject_value* 가 행의 수 또는 비율을 참조 하는지 여부를 결정 합니다.  
  
기본 *reject_value* 는 0입니다.  
  
-Rt 값과 함께 사용 하는 경우, 거부 된 행 수가 reject_value을 초과 하면 로더가 로드를 중지 합니다.  
  
-Rt 백분율을 사용 하는 경우 로더는 간격 (-rs 옵션)에서 백분율을 계산 합니다. 따라서 실패 한 행의 백분율이 *reject_value*를 초과할 수 있습니다.  
  
**-rs** *reject_sample_size*  
`-rt percentage`증분 백분율 검사를 지정 하는 옵션과 함께 사용 됩니다. 예를 들어 reject_sample_size가 1000 인 경우 로더는 1000 행을 로드 하려고 시도한 후 실패 한 행의 백분율을 계산 합니다. 각 추가 1000 행을 로드 하려고 시도한 후 실패 한 행의 백분율을 다시 계산 합니다.  
  
**-c**  
Char, nchar, varchar 및 nvarchar 필드의 왼쪽과 오른쪽에서 공백 문자를 제거 합니다. 공백 문자만 포함 하는 각 필드를 빈 문자열로 변환 합니다.  
  
예제:  
  
' '이 ' ' (으)로 잘렸습니다.  
  
' abc '는 ' abc '로 잘립니다.  
  
-C를-E와 함께 사용 하는 경우-E 작업이 먼저 발생 합니다. 공백 문자만 포함 하는 필드는 NULL이 아닌 빈 문자열로 변환 됩니다.  
  
**-E**  
빈 문자열을 NULL로 변환 합니다. 기본값은 이러한 변환을 수행 하지 않는 것입니다.  
  
**-m**  
로드의 두 번째 단계에서 다중 트랜잭션 모드를 사용 합니다. 준비 테이블에서 분산 테이블로 데이터를 로드 하는 경우  
  
**-M**을 사용 하 여 SQL Server PDW를 수행 하 고 커밋을 병렬로 로드 합니다. 이는 기본 로드 모드 보다 훨씬 더 빠르게 수행 되지만 트랜잭션이 안전 하지 않습니다.  
  
**-M을 사용**하지 않을 경우 SQL Server PDW는 각 계산 노드 내의 배포에서 순차적으로 부하를 수행 하 고 커밋합니다. 이 방법은 다중 트랜잭션 모드 보다 느리지만 트랜잭션을 안전 하 게 보호 합니다.  
  
**-m** 은 *append*, *reload*및 *upsert*의 경우 선택 사항입니다.  
  
fastappend에는 **-m** 이 필요 합니다.  
  
**-m** 은 복제 된 테이블과 함께 사용할 수 없습니다.  
  
**-m** 은 두 번째 로드 단계에만 적용 됩니다. 첫 번째 로드 단계에는 적용 되지 않습니다. 준비 테이블에 데이터를 로드 하는 중입니다.  
  
다중 트랜잭션 모드를 사용 하는 롤백이 없습니다. 즉, 실패 하거나 중단 된 로드에서 복구 하는 작업은 사용자의 부하 프로세스에 의해 처리 되어야 합니다.  
  
빈 테이블로 로드 하는 경우에만 **-m** 을 사용 하 여 데이터 손실 없이 복구할 수 있도록 하는 것이 좋습니다. 로드 실패에서 복구 하려면 대상 테이블을 삭제 하 고, 로드 문제를 해결 하 고, 대상 테이블을 다시 만든 후 로드를 다시 실행 합니다.  
  
**-N**  
대상 어플라이언스에 신뢰할 수 있는 기관의 유효한 SQL Server PDW 인증서가 있는지 확인 합니다. 이를 통해 공격자가 데이터를 도용 하지 않고 권한이 없는 위치로 전송 하는 것을 방지할 수 있습니다. 인증서가 이미 어플라이언스에 설치 되어 있어야 합니다. 인증서를 설치 하는 데 지원 되는 유일한 방법은 어플라이언스 관리자가 Configuration Manager 도구를 사용 하 여 설치 하는 것입니다. 어플라이언스에 신뢰할 수 있는 인증서가 설치 되어 있는지 확실 하지 않은 경우 어플라이언스 관리자에 게 문의 하세요.  
  
**-se**  
빈 파일 로드를 건너뜁니다. 빈 gzip 파일의 압축 풀기도 건너뜁니다.

**-l**  
CU 7.4 update에서 사용할 수 있으며 로드할 수 있는 최대 행 길이 (바이트)를 지정 합니다. 유효한 값은 32768에서 33554432 사이의 정수입니다. 32KB 보다 큰 행을 로드 하는 데 필요한 경우에만를 사용 하 여 클라이언트와 서버에 더 많은 메모리를 할당 합니다.
  
## <a name="return-code-values"></a>반환 코드 값  
0 (성공) 또는 기타 정수 값 (오류)  
  
명령 창이 나 배치 파일에서를 사용 `errorlevel` 하 여 반환 코드를 표시 합니다. 예를 들면 다음과 같습니다.  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
PowerShell을 사용 하는 경우를 사용 `$LastExitCode` 합니다.  
  
## <a name="permissions"></a>사용 권한  
대상 테이블에서 로드 권한 및 해당 사용 권한 (INSERT, UPDATE, DELETE)이 필요 합니다. 준비 데이터베이스에 대 한 CREATE 권한 (임시 테이블을 만드는 경우)이 필요 합니다. 준비 데이터베이스를 사용 하지 않는 경우 대상 데이터베이스에 대 한 CREATE 권한이 필요 합니다. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>일반적인 주의 사항  
Dwloader를 사용 하 여 로드할 때 데이터 형식 변환에 대 한 자세한 내용은 [dwloader의 데이터 형식 변환 규칙](dwloader-data-type-conversion-rules.md)을 참조 하세요.  
  
매개 변수에 하나 이상의 공백이 포함 된 경우 매개 변수를 큰따옴표로 묶습니다.  
  
설치 된 위치에서 로더를 실행 해야 합니다. Dwloader 실행 파일은 기기와 함께 미리 설치 되며 C:\Program Files\Microsoft SQL Server Data Warehouse\DWLoader 디렉터리에 있습니다.  
  
매개 변수 파일 (-f 옵션)에 지정 된 매개 변수를 명령줄 매개 변수로 지정 하 여 재정의할 수 있습니다.  
  
로더 인스턴스를 여러 개 동시에 실행할 수 있습니다. 로더 인스턴스의 최대 수는 미리 구성 되어 있으며 변경할 수 없습니다. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
로드 된 데이터에는 원본 위치 보다 더 많은 공간이 필요할 수 있습니다. 데이터의 하위 집합을 사용 하 여 테스트 가져오기를 수행 하 여 디스크 사용량을 예측할 수 있습니다.  
  
**Dwloader** 는 트랜잭션 프로세스이 고 실패 시 정상적으로 롤백되기 때문에 대량 로드가 성공적으로 완료 되 면 롤백할 수 없습니다. 활성 **dwloader** 프로세스를 취소 하려면 CTRL + C를 입력 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
동시에 발생 하는 모든 로드의 총 크기는 데이터베이스의 LOG_SIZE 보다 작아야 하며, 모든 동시 로드의 총 크기가 LOG_SIZE의 50% 미만인 것이 좋습니다. 이러한 크기 제한을 얻으려면 큰 부하를 여러 일괄 처리로 분할할 수 있습니다. LOG_SIZE에 대 한 자세한 내용은 [CREATE DATABASE](../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016) 를 참조 하세요.  
  
하나의 load 명령을 사용 하 여 여러 파일을 로드할 때 거부 된 모든 행은 동일한 거부 파일에 기록 됩니다. 거부 파일에는 거부 된 각 행이 포함 된 입력 파일이 표시 되지 않습니다.  
  
빈 문자열은 구분 기호로 사용 하면 안 됩니다. 빈 문자열이 행 구분 기호로 사용 되는 경우 로드는 실패 합니다. 열 구분 기호로 사용 하는 경우 로드는 구분 기호를 무시 하 고 계속 해 서 기본 "|"를 열 구분 기호로 사용 합니다. 문자열 구분 기호로 사용 하는 경우 빈 문자열이 무시 되 고 기본 동작이 적용 됩니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
**dwloader** 잠금 동작은 *load_mode_option*에 따라 달라 집니다.  
  
-   **추가** -추가가 권장 및 가장 일반적인 옵션입니다. 추가는 준비 테이블에 데이터를 로드 합니다. 잠금은 아래에 자세히 설명 되어 있습니다.  
  
-   **빠른 추가** -빠른 추가는 ExclusiveUpdate 테이블 잠금을 수행 하는 최종 테이블에 직접 로드 되며, 준비 테이블을 사용 하지 않는 유일한 모드입니다.  
  
-   **다시** 로드-다시 로드는 준비 테이블에 데이터를 로드 하 고 준비 테이블과 최종 테이블 모두에 대해 배타적 잠금이 필요 합니다. 동시 작업에는 다시 로드 하지 않는 것이 좋습니다.  
  
-   **upsert** -upsert은 준비 테이블에 데이터를 로드 한 다음 준비 테이블에서 최종 테이블로 병합 작업을 수행 합니다. Upsert에는 최종 테이블에 대 한 배타적 잠금이 필요 하지 않습니다. Upsert를 사용 하는 경우 성능이 달라질 수 있습니다. 사용자 환경에서 동작을 테스트 합니다.  
  
### <a name="locking-behavior"></a>잠금 동작  
**추가 모드 잠금**  
  
추가는-m 인수를 사용 하 여 다중 트랜잭션 모드에서 실행 될 수 있지만 트랜잭션은 안전 하지 않습니다. 따라서 추가는-m 인수를 사용 하지 않고 트랜잭션 작업으로 사용 되어야 합니다. 그러나 최종 삽입 선택 작업 중에는 트랜잭션 모드가 현재 다중 트랜잭션 모드 보다 약 6 배 느립니다.  
  
추가 모드는 두 단계로 데이터를 로드 합니다. 1 단계에서는 원본 파일에서 준비 테이블로 데이터를 동시에 로드 합니다 (조각화가 발생할 수 있음). 2 단계는 준비 테이블에서 최종 테이블로 데이터를 로드 합니다. 두 번째 단계에서는 **INSERT INTO ... WITH (TABLOCK)** 작업을 선택 합니다. 다음 표에서는 최종 테이블의 잠금 동작과 추가 모드를 사용 하는 경우의 로깅 동작을 보여 줍니다.  
  
|테이블 형식|다중 트랜잭션<br />모드 (-m)|테이블이 비어 있음|동시성이 지원 됨|로깅|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|힙|예|예|예|최소|  
|힙|예|예|예|최소|  
|힙|예|예|예|최소|  
|힙|예|예|예|최소|  
|Cl.exe|예|예|예|최소|  
|Cl.exe|예|예|예|전체|  
|Cl.exe|예|예|예|최소|  
|Cl.exe|예|예|예|전체|  
  
위의 표에서는 추가 모드를 힙 또는 CI (클러스터형 인덱스) 테이블로 로드 하 여 다중 트랜잭션 플래그를 사용 하거나 사용 하지 않고 빈 테이블이 나 비어 있지 않은 테이블에 로드 하는 **dwloader** 를 보여 줍니다. 이러한 각 부하 조합의 잠금 및 로깅 동작이 표에 표시 됩니다. 예를 들어, 추가 모드를 사용 하 여 다중 트랜잭션 모드를 사용 하지 않는 클러스터형 인덱스에 추가 모드를 로드 하 고 빈 테이블로 로드 하는 경우 PDW는 테이블에 대 한 배타적 잠금을 만들고 로깅은 최소화 합니다. 즉, 고객은 두 번째 단계와 쿼리를 빈 테이블로 동시에 로드할 수 없습니다. 그러나 동일한 구성을 사용 하 여 비어 있지 않은 테이블에 로드 하는 경우 PDW는 테이블에 대해 배타 잠금을 실행 하지 않으며 동시성이 가능 합니다. 그러나 전체 로깅이 발생 하 여 프로세스가 느려집니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-simple-dwloader-example"></a>A. Simple dwloader 예  
다음 예에서는 필수 옵션만 선택 하 여 **로더** 를 시작 하는 방법을 보여 줍니다. 기타 옵션은 *loadparamfile.txt*전역 구성 파일에서 가져옵니다.  
  
SQL Server 인증을 사용 하는 예입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
Windows 인증을 사용 하는 동일한 예제입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
소스 파일 및 오류 파일에 인수를 사용 하는 예제입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. AdventureWorks 테이블로 데이터 로드  
다음 예는 **AdventureWorksPDW2012**으로 데이터를 로드 하는 일괄 처리 스크립트의 일부입니다.  전체 스크립트를 보려면 **AdventureWorksPDW2012** 설치 패키지와 함께 제공 되는 aw_create.bat 파일을 엽니다. 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

다음 스크립트 조각에서는 dwloader를 사용 하 여 데이터를 나이 계정 및 나이에 대 한 통화 테이블로 로드 합니다. 이 스크립트는 이더넷 주소를 사용 합니다. InfiniBand를 사용 하는 경우 서버는 *>appliance_name<* 됩니다 `-SQLCTL01` .  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
다음은 나의 계정 테이블에 대 한 DDL입니다.  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
다음은 테이블에 로드할 데이터가 포함 된 데이터 파일 DimAccount.txt의 예입니다.  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. 명령줄에서 데이터 로드  
다음 예제와 같이 명령줄에 모든 매개 변수를 입력 하 여 예 B의 스크립트를 바꿀 수 있습니다.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
명령줄 매개 변수에 대 한 설명입니다.  
  
-   *C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe* 는 dwloader.exe의 설치 된 위치입니다.  
  
-   *-S* 뒤에는 제어 노드의 IP 주소가 옵니다.  
  
-   *-E* 는 빈 문자열을 NULL로 로드 하도록 지정 합니다.  
  
-   *-M reload* 는 원본 데이터를 삽입 하기 전에 대상 테이블을 자르는 방법을 지정 합니다.  
  
-   *-e UTF16* 은 원본 파일이 little endian 문자 인코딩 형식을 사용 함을 나타냅니다.  
  
-   *-i .\DimAccount.txt* 현재 디렉터리에 있는 DimAccount.txt 라는 파일에 있는 데이터를 지정 합니다.  
  
-   *-T AdventureWorksPDW2012* 는 데이터를 받을 테이블의 세 부분으로 구성 된 이름을 지정 합니다.  
  
-   *-R 파일 계정. 잘못* 됨을 지정 하면 로드에 실패 한 행이 나이 계정 이라는 파일에 기록 됩니다.  
  
-   *-t "|"* 입력 파일 DimAccount.txt의 필드가 파이프 문자로 구분 되어 있음을 나타냅니다.  
  
-   *-r \r\n* DimAccount.txt의 각 행을 캐리지 리턴 및 줄 바꿈 문자로 지정 합니다.  
  
-   *-U <login_name>-P <password> * 로드를 수행할 수 있는 권한이 있는 로그인에 대 한 로그인 및 암호를 지정 합니다.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
