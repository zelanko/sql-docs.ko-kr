---
title: dwloader 명령줄 로더-병렬 데이터 웨어하우스 | Microsoft Docs
description: dwloader 병렬 데이터 웨어하우스 (PDW) 명령줄 도구는 기존 테이블에 테이블 행을 대량 로드 하는 경우
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: dd3f005346c5faae9e02513a144d04d80857b770
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961022"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>dwloader 병렬 데이터 웨어하우스에 대 한 명령줄 로더
**dwloader** 는 기존 테이블에 테이블 행을 대량 로드 하는 병렬 데이터 웨어하우스 (PDW) 명령줄 도구입니다. 행을 로드할 때 모든 행을 테이블의 끝에 추가할 수 있습니다 (*추가 모드* 하거나 *fastappend 모드*) 새 행을 추가 하 고 기존 행을 업데이트 (*upsert 모드*), 모든 또는 삭제 행 로드 하기 전에 기존 및 빈 테이블에 모든 행을 삽입 한 다음 (*모드를 다시 로드*).  
  
**데이터를 로드 하기 위한 프로세스**  
  
1.  원본 데이터를 준비 합니다.  
  
    사용자 고유의 ETL 프로세스를 사용 하 여 로드 하려는 원본 데이터를 만듭니다. 원본 데이터는 대상 테이블의 스키마와 일치 하도록 포맷 되어야 합니다. 하나 이상의 텍스트 파일에 원본 데이터를 저장 하 고 로드 서버의 동일한 디렉터리에 텍스트 파일을 복사 합니다. 로드 서버에 대 한 정보를 참조 하세요. [로드 서버 획득 및 구성](acquire-and-configure-loading-server.md)  
  
2.  로드 옵션을 준비 합니다.  
  
    사용 하 여 로드 옵션을 결정 합니다. 구성 파일에서 로드 옵션을 저장 합니다. 로드 서버에서 로컬 위치로 구성 파일을 복사 합니다. 합니다 **dwloader** 구성 옵션은이 항목에서 설명 합니다.  
  
3.  오류 옵션 부하를 준비 합니다.  
  
    하는 방법을 결정 **dwloader** 로드 하지 못한 행을 처리 하 합니다. 로드를 수행 하려면 **dwloader** 먼저 준비 테이블로 데이터를 로드 하 고 대상 테이블에 데이터를 전송 합니다. 준비 테이블로 데이터를 로드 하는 로더를 로드 하지 못한 행의 수를 추적 합니다. 예를 들어 올바르게 포맷 되지 않는 행을 로드 하지 못합니다. 실패 한 행은 거부 파일에 복사 됩니다. 기본적으로 다른 거부 임계값을 지정 하지 않으면 첫 번째 거부 후 로드를 중단 합니다.  
  
4.  설치할 **dwloader**합니다.  
  
    이미 설치 되어 있지 않으면 dwloader 로딩 서버를 설치 합니다. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  실행할 **dwloader**합니다.  
  
    로드 서버에 로그인 하 고 실행 파일 **dwloader.exe** 적절 한 명령줄 옵션을 사용 하 여 합니다.  
  
6.  결과 확인 합니다.  
  
    실패 한 확인할 수 있습니다 (-R을 사용 하 여 지정 됨) 파일 행 참조 하는 경우 행을 모두 로드 하지 못했습니다. 이 파일 비어 있으면 모든 행 로드 했습니다. **dwloader** 경우 실패 (거부 된 행 외)를 실행 하는 모든 단계를 모두 롤백합니다를 초기 상태로 이므로 트랜잭션.  
  
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
로더를 사용 하는 방법에 대 한 간단한 도움말 정보를 표시 합니다. 도움말 없는 다른 명령줄 매개 변수를 지정 하는 경우에 표시 됩니다.  
  
**-U** *login_name*  
로드 하는 데 적절 한 권한이 있는 유효한 SQL Server 인증 로그인 합니다.  
  
**-P** *password*  
SQL Server 인증을 위한 암호 *login_name*합니다.  
  
**-W**  
Windows 인증을 사용합니다. (No *login_name* 하거나 *암호* 필요 합니다.) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
매개 변수 파일을 사용 하 여 *parameter_file_name*, 명령줄 매개 변수 대신 합니다. *parameter_file_name* 를 제외한 모든 명령줄 매개 변수를 포함할 수 있습니다 *user_name* 하 고 *암호*합니다. 매개 변수는 매개 변수 파일에 명령줄에 지정 된 경우 명령줄 file 매개 변수를 재정의 합니다.  
  
매개 변수 파일을 포함 한 매개 변수 없이 합니다 **-** 줄의 접두사입니다.  
  
예를 들면 다음과 같습니다.  
  
`rt=percentage`  
  
`rv=25`  
  
* *-S***target_appliance*  
로드 된 데이터를 받을 SQL Server PDW 어플라이언스를 지정 합니다.  
  
*Infiniband 연결용*, *target_appliance* < 어플라이언스-이름 >으로 지정 됩니다-SQLCTL01 합니다. 이 연결을 명명 된 구성 참조 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)합니다.  
  
이더넷 연결에 대 한 *target_appliance* 제어 노드 클러스터에 대 한 IP 주소입니다.  
  
생략 하면 dwloader dwloader를 설치할 때 지정 된 값으로 기본값은입니다. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [*schema*].*table_name*  
대상 테이블에 대해 세 부분으로 이루어진 이름입니다.  
  
* *-I***source_data_location*  
로드할 하나 이상의 소스 파일의 위치입니다. 각 소스 파일은 텍스트 파일 또는 사용 하 여 gzip 압축 텍스트 파일 이어야 합니다. 각 gzip 파일로 하나의 소스 파일을 압축할 수 있습니다.  
  
소스 파일 형식:  
  
-   소스 파일 로드 옵션에 따라 포맷 되어야 합니다.  
  
-   소스 파일에서 각 줄에 하나의 테이블 행의 데이터를 포함합니다. 원본 데이터는 대상 테이블의 스키마를 일치 해야 합니다. 열 순서 및 데이터 형식도 일치 해야 합니다. 행의 각 필드는 대상 테이블의 열을 나타냅니다.  
  
-   기본적으로 필드는 가변 길이 및 구분 기호로 구분 합니다. 구분 기호 유형을 지정 하려면 < variable_length_column_options > 명령줄 옵션을 사용 합니다. 고정된 길이 필드를 지정 하려면 < fixed_width_column_options > 명령줄 옵션을 사용 합니다.  
  
원본 데이터 위치를 지정 합니다.  
  
-   원본 데이터 위치는 네트워크 경로 또는 로컬 경로 로드 서버의 디렉터리를 수 있습니다.  
  
-   디렉터리의 모든 파일을 지정 하려면 뒤에 디렉터리 경로 입력 합니다 * 와일드 카드 문자입니다.  로더는 원본 데이터 위치에 있는 모든 하위 디렉터리에서 파일을 로드 하지 않습니다. 디렉터리는 gzip 파일에 있는 경우 로더 오류입니다.  
  
-   일부 파일을 디렉터리에 지정 하려면 문자 조합을 사용 하 여 및 * 와일드 카드입니다.  
  
하나의 명령으로 여러 파일을 로드 합니다.  
  
-   모든 파일이 동일한 디렉터리에 있어야 합니다.  
  
-   파일은 모든 텍스트 파일, 모든 gzip 파일 또는 텍스트와 gzip 파일의 조합 이어야 합니다.  
  
-   파일 헤더 정보를 포함할 수 있습니다.  
  
-   모든 파일에는 동일한 문자 인코딩 형식을 사용 해야 합니다. -E 옵션을 참조 하세요.  
  
-   모든 파일은 동일한 테이블에 로드 되어야 합니다.  
  
-   모든 파일 연결 되어 하나의 파일 되며 거부 된 행을 단일 거부 파일로 이동 처럼 로드 됩니다.  
  
예를 들면 다음과 같습니다.  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
로드 오류가 발생 하는 경우 **dwloader** 라는 파일에 오류 정보가 오류 설명 및 로드에 실패 한 행을 저장 *load_failure_file_name*합니다. 이 파일이 이미 있는 경우 dwloader 기존 파일을 덮어쓰게 됩니다. *load_failure_file_name* 첫 번째 오류가 발생 하면 생성 됩니다. 모든 행을 성공적으로 로드 하는 경우 *load_failure_file_name* 만들어지지 않습니다.  
  
**-fh** *number_header_rows*  
줄 (행)의 시작 부분에서 무시할 수 *source_data_file_name*합니다. 기본값은 0입니다.  
  
<variable_length_column_options>  
에 대 한 옵션을 *source_data_file_name* 문자 구분 된 가변 길이 열이 있는 합니다. 기본적으로 *source_data_file_name* 가변 길이 열에 ASCII 문자가 포함 되어 있습니다.  
  
ASCII 파일에 대 한 Null 구분 기호를 연속적으로 배치 하 여 표시 됩니다. 파이프로 구분 된 파일의 예를 들어, ("|"), NULL로 표시 됩니다 "| |"입니다. 쉼표로 구분 된 파일에서 NULL로 표시 됩니다 ",". 또한 합니다 **-E** (-emptyStringAsNull) 옵션을 지정 해야 합니다. -E에 대 한 자세한 내용은 아래를 참조 하세요.  
  
**-e** *character_encoding*  
데이터 파일에서 로드할 데이터에 대 한 문자 인코딩 형식을 지정 합니다. 옵션 (기본값) ASCII, UTF8, UTF16, 또는 UTF16BE, 여기서 UTF16 약간 endian 이며 UTF16BE big endian 됩니다. 이러한 옵션은 대/소문자 구분 합니다.  
  
**-t** *field_delimiter*  
행의 각 필드 (열)에 대 한 구분 기호입니다. 필드 구분 기호는 ASCII 이스케이프 문자 또는 ASCII 16 진수 값이 하나 이상입니다.  
  
|이름|이스케이프 문자|16 진수 문자|  
|--------|--------------------|-----------------|  
|탭|\t|0x09|  
|캐리지 리턴 (CR)|\r|0x0d|  
|줄 바꿈 (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|쉼표|','|0x2c|  
|큰따옴표|\\"|0x22|  
|작은따옴표|\\'|0x27|  
  
명령줄에서 파이프 문자를 지정 하려면 큰따옴표를 사용 하 여 묶습니다 "|"입니다. 명령줄 구문 분석기에서 잘못 해석을 피해 야 합니다. 다른 문자는 작은따옴표를 사용 하 여로 묶습니다.  
  
예를 들면 다음과 같습니다.  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t '~|~'  
  
**-r** *row_delimiter*  
원본 데이터 파일의 각 행에 대 한 구분 기호입니다. 하나 이상의 ASCII 값이 행 구분 기호가입니다.  
  
캐리지 리턴 (CR), 줄 바꿈 (LF) 또는 탭 문자 구분 기호를 지정 하려면 이스케이프 문자 (\r, \n \t) 또는 16 진수 값 (x 0, 0 d, 09)를 사용할 수 있습니다. 구분 기호로 다른 특수 문자를 지정 하려면 해당 16 진수 값을 사용 합니다.  
  
CR LF가 +의 예:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR의 예:  
  
-r \r  
  
-r 0x0d  
  
LF의 예:  
  
-r \n  
  
-r 0x0a  
  
LF가 Unix 필요 합니다. CR을 Windows에 필요 합니다.  
  
**-s** *string_delimiter*  
문자열 데이터의 구분 기호로 분리 된 텍스트 입력된 파일의 필드를 입력 합니다. 하나 이상의 ASCII 값이 문자열 구분 기호가입니다.  문자로 지정할 수 있습니다 (예:-s *) 또는 16 진수 값 (예:-s 0x22 큰따옴표에 대 한).  
  
예를 들면 다음과 같습니다.  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options>  
고정 길이 열이 있는 원본 데이터 파일에 대 한 옵션입니다. 기본적으로 *source_data_file_name* 가변 길이 열에 ASCII 문자가 포함 되어 있습니다.  
  
-E UTF8 인지 확인 하는 경우에 고정된 폭 열 지원 되지 않습니다.  
  
**-w** *fixed_width_config_file*  
경로 및 각 열의 문자 수를 지정 하는 구성 파일의 이름입니다. 모든 필드를 지정 해야 합니다.  
  
이 파일은 로드 서버에 있어야 합니다. 경로 UNC 상대 또는 절대 경로일 수 있습니다. 각 줄 *fixed_width_config_file* 해당 열에 대 한 열 및 문자 수의 이름을 포함 합니다. 다음과 같이 각 열 마다 한 줄이 및 파일의 순서는 대상 테이블의 순서와 일치 해야 합니다.  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
고정 폭 config 파일 예제:  
  
SalesCode=3  
  
SalesID=10  
  
예제에서 줄 *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
이전 예제에서는 로드 된 첫 번째 행을 갖습니다 SalesCode '230' 및 SalesID = = 'Shirts0056'. 두 번째 로드 된 행 SalesCode 해야 합니다. '' 줄어들고 SaleID = = 'Towels1356'.  
  
선행 및 후행 공백이 나 데이터 형식 변환 고정된 폭 모드로 처리 하는 방법에 대 한 자세한 내용은 [데이터 형식 변환 규칙 dwloader](dwloader-data-type-conversion-rules.md)합니다.  
  
**-e** *character_encoding*  
데이터 파일에서 로드할 데이터에 대 한 문자 인코딩 형식을 지정 합니다. 옵션 (기본값) ASCII, UTF8, UTF16, 또는 UTF16BE, 여기서 UTF16 약간 endian 이며 UTF16BE big endian 됩니다. 이러한 옵션은 대/소문자 구분 합니다.  
  
-E UTF8 인지 확인 하는 경우에 고정된 폭 열 지원 되지 않습니다.  
  
**-r** *row_delimiter*  
원본 데이터 파일의 각 행에 대 한 구분 기호입니다. 하나 이상의 ASCII 값이 행 구분 기호가입니다.  
  
캐리지 리턴 (CR), 줄 바꿈 (LF) 또는 탭 문자 구분 기호를 지정 하려면 이스케이프 문자 (\r, \n \t) 또는 16 진수 값 (x 0, 0 d, 09)를 사용할 수 있습니다. 구분 기호로 다른 특수 문자를 지정 하려면 해당 16 진수 값을 사용 합니다.  
  
CR LF가 +의 예:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR의 예:  
  
-r \r  
  
-r 0x0d  
  
LF의 예:  
  
-r \n  
  
-r 0x0a  
  
LF가 Unix 필요 합니다. CR을 Windows에 필요 합니다.  
  
**-D** {0} **ymd** | ydm | mdy | myd |  dmy | dym | *custom_date_format* }  
입력된 파일에서 월 (m), (d), 일 및 연도 (y) 모든 날짜/시간 필드에 대 한 순서를 지정합니다. 기본 순서는 ymd 합니다. 동일한 소스 파일에 대 한 여러 주문 형식을 지정 하려면-dt 옵션을 사용 합니다.  
  
ymd | dmy  
ydm 및 dmy 동일한 입력된 형식을 허용합니다. 둘 다를 시작 또는 끝 날짜의 연도 허용 합니다. 예를 들어, 둘 다에 대해 **ydm** 하 고 **dmy** 날짜 형식, 2013-02-03 또는 02-03-2013 입력된 파일에 있을 수 있습니다.  
  
ydm  
데이터 형식 datetime 및 smalldatetime 열으로 ydm으로 서식이 지정 된 입력만 로드할 수 있습니다. Ydm 값을 datetimeoffset 데이터 형식, 날짜 또는 datetime2 열에 로드할 수 없습니다.  
  
mdy  
mdy 허용 <month> <space> <day> <comma> <year>합니다.  
  
Mdy 1975 년 1 월 1 년에 대 한 입력된 데이터의 예:  
  
-   1975 년 1 월 1 년  
  
-   75 년 1 월 1 일,  
  
-   1 월 1 일/1/75  
  
-   01011975  
  
myd  
3 월에 대 한 파일 예제 입력 04,2010: 03-2010-04, 3/2010/4  
  
dym  
2010 년 3 월 4 일에 대 한 입력된 파일 예제: 04-2010-03, 4/2010/3  
  
*custom_date_format*  
*custom_date_format* 은 사용자 지정 날짜 형식 (예를 들어, MM/dd/yyyy) 이전 버전과 호환성만 포함 합니다. dwloader는 사용자 지정 날짜 형식을 적용 하지 않습니다. 대신를 사용자 지정 날짜 형식으로 지정 하면 **dwloader** ymd, ydm, mdy, myd, dym, 나 dmy의 해당 설정으로 변환 됩니다.  
  
예를 들어,-D MM/dd/yyyy를 지정 하면 모든 날짜를 월을 사용 하 여 먼저 입력 한 일 및 연도 (mdy) 다음 dwloader 필요 합니다. 문자를 2 월, 2 자리 일 및 사용자 지정 날짜 형식으로 지정 된 대로 4 자리 연도는 적용 하지 않습니다. 날짜 형식은-D MM/dd/yyyy 하는 경우 입력된 파일에서 날짜 서식을 지정할 수는 방법의 몇 가지 예는 다음과 같습니다. 2013/01/02, Jan.02.2013, 2013 년 1 월 2  
  
보다 포괄적인 서식 지정 정보를 참조 하세요 [데이터 형식 변환 규칙 dwloader](dwloader-data-type-conversion-rules.md)합니다.  
  
**-dt** *datetime_format_file*  
각 날짜/시간 형식 이라는 파일에 지정 된 *datetime_format_file*합니다. 명령줄 매개 변수를 달리 큰따옴표로 공백을 포함 하는 파일 매개 변수 하지 묶어야 합니다. 데이터를 로드 하는 대로 날짜/시간 형식을 변경할 수 없습니다. 원본 데이터 파일 및 대상 테이블의 해당 열에는 동일한 형식을 이어야 합니다.  
  
각 줄에는 대상 테이블에 날짜/시간 형식으로 열의 이름을 포함합니다.  
  
예를 들면 다음과 같습니다.  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
준비 테이블을 포함 하는 데이터베이스 이름입니다. 기본값은 대상 테이블에 대 한 데이터베이스가-T 옵션을 사용 하 여 지정 된 데이터베이스입니다. 준비 데이터베이스를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [스테이징 데이터베이스를 만들](staging-database.md)합니다.  
  
**-M** *load_mode_option*  
Upsert를 추가 또는 데이터를 다시 로드할 것인지 지정 합니다. 기본 모드를 추가 합니다.  
  
추가  
로더는 대상 테이블의 기존 행의 끝에 행을 삽입합니다.  
  
fastappend  
로더 대상 테이블의 기존 행의 끝에 임시 테이블을 사용 하지 않고 직접 행을 삽입 합니다. fastappend 다중 트랜잭션 필요 (-m) 옵션입니다. Fastappend를 사용 하는 경우 스테이징 데이터베이스를 지정할 수 없습니다. Fastappend 복구 실패 했거나 중단 된 부하에서 고유한 로드 프로세스에서 처리 해야 하는 사용 하 여 롤백이 발생 하지 않은 경우  
  
upsert **-K**  *merge_column* [ ,...*n* ]  
로더가는 SQL Server 병합 문을 사용 하 여 기존 행을 업데이트 하 고 새 행을 삽입 합니다.  
  
-K 옵션에는 병합의 기준 열을 지정 합니다. 이러한 열이 고유한 행을 표시 해야 하는 병합 키를 형성 합니다. 병합 키가 대상 테이블의 행이 업데이트 됩니다. 대상 테이블에 병합 키가 없으면 행이 추가 됩니다.  
  
해시 분산 테이블에 대 한 병합 키 이거나 배포 열을 포함 합니다.  
  
복제 된 테이블에 대 한 병합 키는 하나 이상의 열을 결합 합니다. 이러한 열은 응용 프로그램의 필요에 따라 지정 됩니다.  
  
공백 없이 쉼표로 구분 된 공간을 사용 하 여 쉼표로 구분 된 및 작은따옴표로 묶인 여러 열 이어야 합니다.  
  
원본 테이블의 두 행 일치 하는 병합 키 값이 있는 경우 각 해당 행이 동일 해야 합니다.  
  
다시 로드  
로더는 원본 데이터를 삽입 하기 전에 대상 테이블을 자릅니다.  
  
**-b** *batchsize*  
Microsoft 지원에 사용 권장 *batchsize* DMS 계산 노드의 SQL Server 인스턴스로 수행 하는 대량 복사를 위한 SQL Server 일괄 처리 크기입니다.  때 *batchsize* 지정 된 경우 SQL Server PDW에서 각 부하에 대 한 동적으로 계산 되는 일괄 처리 부하 크기를 재정의 합니다.  
  
SQL Server 2012 PDW 부터는 제어 노드에 동적으로 계산 각 부하에 대 한 일괄 처리 크기를 기본적으로 합니다. 이 자동 계산 메모리 크기, 대상 테이블 형식, 대상 테이블 스키마, 유형, 파일 크기 및 사용자의 리소스 클래스와 같은 여러 매개 변수를 기반으로 합니다.  
  
예를 들어 부하 모드가 FASTAPPEND 테이블에 클러스터형된 columnstore 인덱스를 SQL Server PDW는 rowgroup 닫히게 있도록 1,048,576는 일괄 처리 크기를 사용 하려고 하는 기본 및 직접 로드 하 여 columnstore로 이동 하지 않고도 합니다 델타 저장소입니다. 메모리는 1,048,576는 일괄 처리 크기를 허용 하지 않으면, dwloader 작은 batchsize를 선택 합니다.  
  
부하 유형이 FASTAPPEND, 합니다 *batchsize* 그렇지 않은 경우 테이블에 데이터 로드에 적용 됩니다 *batchsize* 준비 테이블로 데이터 로드에 적용 됩니다.  
  
<reject_options>  
로더를 사용 하면 로드 실패 수를 확인 하기 위한 옵션을 지정 합니다. 로드 실패 임계값을 초과 하는 경우 로더 중지를 업데이트 하 고 모든 행을 커밋하지 됩니다.  
  
**-rt** {0} **값** | 백분율}  
지정 여부를-*reject_value* 에 **-rv** *reject_value* 옵션은 행 (값)의 숫자 리터럴 또는 (백분율) 오류의 비율입니다. 기본값은 값입니다.  
  
배율 옵션은-rs 옵션에 따라 간격으로 발생 하는 실시간으로 계산 합니다.  
  
예를 들어 100 개 행 및 25 로드 로더 하려고 하면 실패 하는 경우 75 성공 실패율은 25%입니다.  
  
**-rv** *reject_value*  
부하를 중단 하기 전까지 허용 개수 또는 행 거부의 비율을 지정 합니다. 합니다 **-rt** 옵션을 결정 하는 경우 *reject_value* 행 개수 또는 행의 비율을 가리킵니다.  
  
기본값 *reject_value* 은 0입니다.  
  
-Rt 값을 사용 하는 경우 거부 된 행 개수 reject_value를 초과 하는 경우 로더가 로드를 중지 합니다.  
  
-Rt 비율을 사용 하 여 사용 하는 경우, 간격 비율을 계산 하는 로더 (-rs 옵션). 따라서 실패 한 행의 비율을 초과할 수 있습니다 *reject_value*합니다.  
  
**-rs** *reject_sample_size*  
사용 된 `-rt percentage` 증분 백분율 검사를 지정 하는 옵션입니다. 예를 들어 reject_sample_size 1000 인 경우 행 1000 개의 로드를 시도한 후 로더 실패 한 행의 백분율이 계산 됩니다. 다시 각 추가로 행 1000 개의 로드를 시도한 후 실패 한 행의 비율을 계산 합니다.  
  
**-t**  
Char, nchar, varchar 및 nvarchar 필드의 왼쪽 및 오른쪽에서 공백 문자를 제거합니다. 빈 문자열에 공백 문자만 포함 하는 각 필드를 변환 합니다.  
  
예를 들면 다음과 같습니다.  
  
' '를 잘린 '  
  
'abc'는 'abc' 잘립니다.  
  
-C-E를 함께 사용할 경우-E 작업이 먼저 발생 합니다. 공백 문자만 포함 하는 필드는 NULL이 아닌 빈 문자열인 경우에 변환 됩니다.  
  
**-E**  
빈 문자열을 NULL로 변환 합니다. 이러한 변환을 수행 하지 하는 기본값은입니다.  
  
**-m**  
다중 트랜잭션 모드를 사용 하 여 로드;의 두 번째 단계 경우 분산된 테이블에 준비 테이블에서 데이터를 로드 합니다.  
  
사용 하 여 **-m**, SQL Server PDW 수행 및 병렬에서 로드를 커밋합니다. 이 기본 모드에서 로드 보다 훨씬 더 빠르게 수행 하지만 트랜잭션 안전 하지 않습니다.  
  
없이 **-m**, SQL Server PDW 수행 하 고 각 계산 노드에 배포 하 고 동시에 계산 노드 간에 로드를 순차적으로 커밋합니다. 이 메서드는 다중 트랜잭션 모드 보다 느리지만 있지만 트랜잭션 안전성이 있습니다.  
  
**-m** 사항임 *추가*를 *다시 로드*, 및 *upsert*합니다.  
  
**-m** fastappend에 필요 합니다.  
  
**-m** 복제 된 테이블을 사용 하 여 사용할 수 없습니다.  
  
**-m** 두 번째 로드 단계에만 적용 됩니다. 첫 번째 로드 단계;에 적용 되지 않습니다. 준비 테이블로 데이터를 로드 합니다.  
  
복구 실패 했거나 중단 된 부하에서 고유한 로드 프로세스에서 처리 해야 하는 다중 트랜잭션 모드를 사용 하 여 롤백이 발생 하지 않은 경우  
  
사용 하는 것이 좋습니다 **-m** 데이터 손실 없이 복구할 수 있도록 빈 테이블을 로드 하는 경우에 합니다. 로드 실패에서 복구 하려면: 대상 테이블을 삭제, 부하 문제를 해결, 대상 테이블 다시 만들기 및 부하를 다시 실행 합니다.  
  
**-N**  
대상 어플라이언스에 신뢰할 수 있는 기관에서 유효한 SQL Server PDW 인증서를 확인 합니다. 데이터 되 고 있지 않습니다을 보장 하는 데 사용할 공격자에 의해 하이재킹 하 고 권한이 없는 위치로 전송 합니다. 인증서 어플라이언스에 이미 설치 되어 있어야 합니다. 인증서를 설치 하는 지원 되는 유일한 방법은 Configuration Manager 도구를 사용 하 여 설치 하도록 어플라이언스 관리자입니다. 어플라이언스 관리자에 문의 하는 경우 알 수 없는 어플라이언스 설치 된 신뢰할 수 있는 인증서에 있는지 여부.  
  
**-se**  
빈 파일 로드를 건너뜁니다. 이 또한 압축을 푸는 작업 빈 gzip 파일을 건너뜁니다.

**-l**  
CU7.4 업데이트를 사용 하 여 사용 가능한 최대 행의에서 길이 (바이트) 로드할 수 있는 지정 합니다. 유효한 값은 32768 33554432 사이의 정수입니다. 클라이언트와 서버에서 더 많은 메모리를 할당 하는이 처럼 큰 행 (32KB 보다 큼)를 로드 하려면 필요한 경우에 사용 합니다.
  
## <a name="return-code-values"></a>반환 코드 값  
0 (성공) 또는 다른 정수 값 (실패)  
  
명령 창 또는 일괄 처리 파일을 사용 하 여 `errorlevel` 반환 코드를 표시 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
PowerShell을 사용 하는 경우 사용 하 여 `$LastExitCode`입니다.  
  
## <a name="permissions"></a>사용 권한  
부하 권한과 대상 테이블에 적용 가능한 사용 권한 (INSERT, UPDATE, DELETE)에 필요합니다. 준비 데이터베이스 만들기 권한 (임시 테이블 만들기)에 필요 합니다. 준비 데이터베이스를 사용 하지 않으면 CREATE 권한이 대상 데이터베이스에 필요 합니다. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>일반적인 주의 사항  
Dwloader로 로드할 때 데이터 형식 변환에 대 한 내용은 참조 하세요 [데이터 형식 변환 규칙 dwloader](dwloader-data-type-conversion-rules.md)합니다.  
  
매개 변수 하나 이상의 공백이 포함 된 경우 큰따옴표를 사용 하 여 매개 변수를 묶어야 합니다.  
  
설치 된 위치에서 로더를 실행 해야 합니다. 실행 dwloader 어플라이언스를 사용 하 여 사전 설치 됩니다 및 C:\Program Files\Microsoft SQL Server 데이터 Warehouse\DWLoader 디렉터리에 위치 합니다.  
  
매개 변수 파일에 지정 된 매개 변수를 재정의할 수 있습니다 (-f 옵션)를 명령줄 매개 변수로 지정 합니다.  
  
로더의 여러 인스턴스를 동시에 실행할 수 있습니다. 로더 인스턴스의 최대 수는 미리 구성 및 변경할 수 없습니다. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
로드 된 데이터 보다는 원본 위치에 어플라이언스의 공간을 더 많이 또는 적게 필요할 수 있습니다. 디스크 사용량을 예측 하는 데이터의 하위 집합을 사용 하 여 테스트 가져오기를 수행할 수 있습니다.  
  
하지만 **dwloader** 트랜잭션 프로세스 롤백됩니다 정상적으로 실패 한 경우, 대량 로드가 성공적으로 완료 되 면 다시 롤백할 수 없습니다. 활성 취소할 **dwloader** 처리, CTRL + C를 입력 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
데이터베이스에 대해 LOG_SIZE 보다 작아야 하며 모든 동시 로드의 전체 크기는 것이 좋습니다 동시에 발생 하는 모든 로드의 총 크기는 LOG_SIZE의 50% 미만인 경우 이 크기 제한을 달성 하려면 여러 일괄 처리로 큰 부하를 분할할 수 있습니다. LOG_SIZE에 대 한 자세한 내용은 참조 하세요. [데이터베이스 만들기](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
하나의 부하 명령 사용 하 여 여러 파일을 로드할 때 모든 거부 된 행은 동일한 거부 파일에 기록 됩니다. 거부 파일에서 각 거부 된 행을 포함 하는 입력된 된 파일을 표시 되지 않습니다.  
  
빈 문자열을 구분 기호로 쓰일 수 없습니다. 빈 문자열은 행 구분 기호로 사용 하는 경우 로드에 실패 합니다. 열 구분 기호로 사용 하는 경우 부하 구분 기호를 무시 하 고 계속 기본값을 사용 하 여 "|" 열 구분 기호로 합니다. 문자열 구분 기호로 사용 하는 경우 빈 문자열은 무시 됩니다 하 고 기본 동작이 적용 됩니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
**dwloader** 잠금 동작에 따라 달라 집니다 합니다 *load_mode_option*합니다.  
  
-   **추가** -추가 되며 권장 되는 가장 일반적인 옵션입니다. 준비 테이블로 데이터 로드를 추가 합니다. 잠금 아래에서 자세히 설명 되어 있습니다.  
  
-   **빠른 추가** -빠른 추가 ExclusiveUpdate 테이블 잠금을 수행 하는 최종 테이블에 직접 로드 되 고 준비 테이블을 사용 하지 않는 유일한 모드입니다.  
  
-   **다시 로드** -다시 로드 준비 테이블로 데이터를 로드 하 고 준비 테이블 및 최종 테이블 모두에서 배타적 잠금이 필요 합니다. 다시 로드 동시 작업에 대 한 권장 되지 않습니다.  
  
-   **upsert** -Upsert 준비 테이블로 데이터를 로드 한 후 최종 테이블에 준비 테이블에서 병합 작업을 수행 합니다. Upsert 최종 테이블에 배타적 잠금이 필요 하지 않습니다. Upsert를 사용 하는 경우 성능이 달라질 수 있습니다. 사용자 환경에서 동작을 테스트 합니다.  
  
### <a name="locking-behavior"></a>잠금 동작  
**모드 잠금 추가**  
  
추가 트랜잭션 안전한 것만 (-m 인수를 사용 하 여) 다중 트랜잭션 모드에서 실행할 수 있습니다. 따라서 추가 (-m 인수 사용) 하지 않고 트랜잭션 작업으로 사용 해야 합니다. 그러나 최종 INSERT SELECT 작업 동안 트랜잭션 모드는 다중 트랜잭션 모드를 보다 현재 약 6 배 느립니다.  
  
추가 모드는 두 단계로 데이터를 로드합니다. 1 단계는 준비 테이블에 동시에 (조각화가 발생할 수 있습니다.) 소스 파일에서 데이터를 로드 합니다. 2 단계는 최종 테이블에 준비 테이블에서 데이터를 로드합니다. 두 번째 단계를 수행는 **INSERT INTO... 선택 WITH (TABLOCK)** 작업 합니다. 다음 표에서 최종 테이블에서 잠금 동작을 보여 줍니다. 및 로깅 동작을 사용 하는 경우 추가 모드:  
  
|테이블 형식|다중 트랜잭션<br />모드 (-m)|테이블이 비어 있음|지원 되는 동시성|로깅|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|힙|예|예|예|최소|  
|힙|예|아니요|예|최소|  
|힙|아니요|사용자 계정 컨트롤|아니요|최소|  
|힙|아니요|아니요|아니요|최소|  
|Cl|예|예|아니요|최소|  
|Cl|예|아니요|예|전체|  
|Cl|아니요|사용자 계정 컨트롤|아니요|최소|  
|Cl|아니요|아니요|예|전체|  
  
위의 표와 **dwloader** 힙 또는 클러스터형된 인덱스 (CI) 테이블 없이 다중 트랜잭션 플래그를 사용 하 여 로드 하 고 빈 테이블 또는 비어 있지 않은 테이블로 로드 추가 모드를 사용 합니다. 잠금 및 부하의 이러한 조합은 각각의 동작을 로깅 테이블에 표시 됩니다. 예를 들어, (2) 단계 추가 모드를 사용 하 여 로드 빈 및 다중 트랜잭션 모드 없이 클러스터형 인덱스로 테이블은 PDW 테이블에 배타적 잠금을 만들 있고 로깅을 최소화 됩니다. 즉, 고객은 빈 테이블로 (2) 단계 및 쿼리를 동시에 로드할 수 없습니다. 그러나 테이블에 대 한 배타적 잠금을 비어 있지 않은 테이블에 동일한 구성을 사용 하 여 로드할 때 PDW 발행할 수 없습니다 및 동시성 가능 합니다. 그러나 전체 로깅이 발생 프로세스 속도 저하.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-dwloader-example"></a>A. 간단한 dwloader 예제  
다음 예제에서는 시작 합니다 **로더** 선택한 필수 옵션을 사용 하 여 합니다. 전역 구성 파일에서 사용 되는 기타 옵션 *loadparamfile.txt*합니다.  
  
SQL Server 인증을 사용 하는 예입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
Windows 인증을 사용 하 여 동일한 예제입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
오류 파일을 소스 파일에 대 한 인수를 사용 하는 예입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>2\. AdventureWorks 테이블에 데이터 로드  
다음 예제에서는 데이터를 로드 하는 배치 스크립트의 일부인 **AdventureWorksPDW2012**합니다.  전체 스크립트를 보려면 사용 하 여 제공 되는 압축을 푼 aw_create.bat 파일을 엽니다는 **AdventureWorksPDW2012** 설치 패키지입니다. 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

다음 스크립트 코드 조각을 dwloader를 사용 하 여 DimAccount 하 고 DimCurrency 테이블에 데이터를 로드 합니다. 이 스크립트는 이더넷 주소를 사용 합니다. InfiniBand를 사용 하 던 서버 것 *< appliance_name >* `-SQLCTL01`합니다.  
  
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
  
다음은 DimAccount 테이블에 대 한 DDL입니다.  
  
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
  
다음은 DimAccount.txt DimAccount 테이블로 로드 하는 데이터가 포함 된 데이터 파일의 예입니다.  
  
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
  
### <a name="c-load-data-from-the-command-line"></a>3\. 명령줄에서 데이터를 로드 합니다.  
예 B의 스크립트는 다음 예와에서 같이 명령줄에서 모든 매개 변수를 입력 하 여 바꿀 수 있습니다.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
명령줄 매개 변수 설명:  
  
-   *C:\Program Files\Microsoft SQL Server 병렬 데이터 Warehouse\100\dwloader.exe* dwloader.exe의 설치 된 위치입니다.  
  
-   *-S* 제어 노드의 IP 주소가 옵니다.  
  
-   *-E* 빈 문자열이 NULL로 로드 하도록 지정 합니다.  
  
-   *-M 다시 로드* 원본 데이터를 삽입 하기 전에 대상 테이블을 자를 지정 합니다.  
  
-   *-e UTF16* 소스 파일 사용 된 little endian 문자 인코딩 형식을 나타냅니다.  
  
-   *-i.\DimAccount.txt* DimAccount.txt 현재 디렉터리에 있는 라는 파일에 데이터를 지정 합니다.  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount* 데이터를 받는 테이블의 세 부분으로 이루어진 이름을 지정 합니다.  
  
-   *-R DimAccount.bad* 로드 하지 못한 행 DimAccount.bad 라는 파일에 기록 됩니다 지정 합니다.  
  
-   *-t "|"*  나타냅니다 DimAccount.txt, 입력된 파일의 필드는 파이프 문자로 구분 됩니다.  
  
-   *-r \r\n* DimAccount.txt의 각 행을 캐리지 리턴으로 종료 하 고 줄 바꿈 문자를 지정 합니다.  
  
-   *-U < >-P login_name <password>*  로그인 및 로드를 수행 하려면 권한이 있는 로그인에 대 한 암호를 지정 합니다.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
