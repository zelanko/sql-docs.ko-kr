---
title: dwloader 병렬 데이터 웨어하우스에 대 한 명령줄 로더
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: '**dwloader** 는 기존 테이블에 대량으로 테이블 행을 로드 하는 병렬 데이터 웨어하우스 (PDW) 명령줄 도구입니다.'
ms.date: 11/04/2016
ms.topic: article
ms.assetid: f79b8354-fca5-41f7-81da-031fc2570a7c
caps.latest.revision: 90
ms.openlocfilehash: 83d04928aa0c8f7fe0156f557466edccc36470dd
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="dwloader-command-line-loader"></a>dwloader 명령줄 로더
**dwloader** 는 기존 테이블에 대량으로 테이블 행을 로드 하는 병렬 데이터 웨어하우스 (PDW) 명령줄 도구입니다. 행을 로드할 때 테이블의 끝에 모든 행을 추가할 수 있습니다 (*추가 모드* 또는 *fastappend 모드*), 새 행이 추가 및 기존 행을 업데이트 (*upsert 모드*)을 모두 삭제 하거나 행 로드 하기 전에 기존 한 다음 빈 테이블에 모든 행을 삽입 (*모드를 다시 로드*).  
  
**데이터를 로드 하기 위한 프로세스**  
  
1.  원본 데이터를 준비 합니다.  
  
    로드 하려는 원본 데이터를 만들려면 사용자가 소유한 ETL 프로세스를 사용 합니다. 원본 데이터는 대상 테이블의 스키마와 일치 하도록 형식 이어야 합니다. 하나 이상의 텍스트 파일에 원본 데이터를 저장 및 로드 서버에 동일한 디렉터리에 텍스트 파일을 복사 합니다. 서버를 로드 하는 방법에 대 한 정보를 참조 하세요. [를 획득 하 고 로드 하는 서버 구성](acquire-and-configure-loading-server.md)  
  
2.  로드 옵션을 준비 합니다.  
  
    사용 하 여 어떤 로드 옵션을 결정 합니다. 구성 파일에서 로드 옵션을 저장 합니다. 구성 파일을 로드 서버의 로컬 위치에 복사 합니다. **dwloader** 구성 옵션은이 항목에서 설명 합니다.  
  
3.  오류 옵션 부하를 준비 합니다.  
  
    어떻게 결정 **dwloader** 로드에 실패 하는 행을 처리 하 합니다. 로드를 수행 하려면 **dwloader** 먼저 준비 테이블로 데이터를 로드 한 후 대상 테이블에 데이터를 전송 합니다. 준비 테이블로 데이터를 로드 하는 로더를 될 때 로드에 실패 하는 행 수를 추적 합니다. 예를 들어 행 올바르게 포맷 되지 않는 로드 되지 것입니다. 실패 한 행은 거부 파일에 복사 됩니다. 기본적으로 부하 다른 거부 임계값을 지정 하지 않으면 첫 번째 거부 한 후 중단 합니다.  
  
4.  설치 **dwloader**합니다.  
  
    아직 설치 되지 않은 경우 dwloader 로드 서버를 설치 합니다. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  실행 **dwloader**합니다.  
  
    로드 서버에 로그인 하 고 실행 파일을 **dwloader.exe** 적절 한 명령줄 옵션을 사용 합니다.  
  
6.  결과 확인 합니다.  
  
    실패 한 확인할 수 있습니다 (-r 지정 됨) 파일 행을 행 로드를 실패 한 경우를 확인 합니다. 이 파일에 수식이 있으면 모든 행 성공적으로 로드 합니다. **dwloader** 는 트랜잭션 단위로, 실패 (다른 거부 된 행 보다)를 실행 하는 모든 단계를 모두 롤백합니다를 초기 상태로 있습니다.  
  
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
}  
```  
  
## <a name="arguments"></a>인수  
**-h**  
로더를 사용 하는 방법에 대 한 간단한 도움말 정보를 표시 합니다. 도움말 다른 명령줄 매개 변수가 지정 된 경우에 표시 됩니다.  
  
**-U** *login_name*  
부하를 수행 하려면 적절 한 권한이 있는 유효한 SQL Server 인증 로그인 합니다.  
  
**-P** *password*  
SQL Server 인증에 대 한 암호 *login_name*합니다.  
  
**-W**  
Windows 인증을 사용합니다. (아니요 *login_name* 또는 *암호* 필요 합니다.) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
매개 변수 파일을 사용 하 여 *parameter_file_name*, 명령줄 매개 변수 대신 합니다. *parameter_file_name* 제외한 모든 명령줄 매개 변수를 포함할 수 있습니다 *user_name* 및 *암호*합니다. 명령줄에서 및 매개 변수 파일에는 형식이 지정 하는 경우 명령줄 file 매개 변수를 재정의 합니다.  
  
매개 변수 파일 없이 하나의 매개 변수가 포함 되어는 **-** 줄당 접두사입니다.  
  
예:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S***target_appliance*  
로드 된 데이터를 받을 SQL Server PDW 어플라이언스를 지정 합니다.  
  
*Infiniband 연결에 대 한*, *target_appliance* < 응용 프로그램 이름 >으로 지정 된-SQLCTL01 합니다. 이 연결에 명명 된 구성 하려면 참조 [InfiniBand 네트워크 어댑터 구성](configure-infiniband-network-adapters.md)합니다.  
  
이더넷 연결에 대 한 *target_appliance* 컨트롤 노드 클러스터에 대 한 IP 주소입니다.  
  
생략 하면 dwloader dwloader가 설치 될 때 지정 된 값에는 기본값입니다. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.*[*schema*].*table_name*  
대상 테이블에 대 한 세 부분으로 이루어진 이름입니다.  
  
**-I***source_data_location*  
로드할 하나 이상의 소스 파일의 위치입니다. 각 소스 파일은 텍스트 파일이 나 gzip을 사용 하 여 압축 된 텍스트 파일 이어야 합니다. 각 gzip 파일에 하나의 원본 파일을 압축할 수 있습니다.  
  
소스 파일 형식을 지정 합니다.  
  
-   로드 옵션에 따라 소스 파일 형식 이어야 합니다.  
  
-   소스 파일의 각 줄에는 하나의 테이블 행에 대 한 데이터가 포함 됩니다. 원본 데이터에는 대상 테이블의 스키마와 일치 해야 합니다. 열 순서 및 데이터 형식을 일치 해야 합니다. 행의 각 필드는 대상 테이블의 열을 나타냅니다.  
  
-   기본적으로 구분 기호로 분리 및 필드가 가변 길이입니다. 구분 기호 유형을 지정 하려면 < variable_length_column_options > 명령줄 옵션을 사용 합니다. 고정된 길이 필드를 지정 하려면 < fixed_width_column_options > 명령줄 옵션을 사용 합니다.  
  
다음 원본 데이터 위치를 지정 하려면  
  
-   네트워크 경로 또는 로컬 경로 로드 서버의 디렉터리를 원본 데이터 위치 수 있습니다.  
  
-   디렉터리에 있는 모든 파일을 지정 하려면 다음 디렉터리 경로 입력의 * 와일드 카드 문자입니다.  로더 원본 데이터 위치에 있는 모든 하위 디렉터리에서 파일을 로드 하지 않습니다. 로더 오류 gzip 파일의 디렉터리가 존재 하는 경우입니다.  
  
-   일부 파일을 디렉터리를 지정 하려면 문자 조합을 사용 하 여 및 * 와일드 카드입니다.  
  
로드 하려면 하나의 명령으로 여러 파일:  
  
-   모든 파일이 동일한 디렉터리에 있어야 합니다.  
  
-   파일은 모든 텍스트 파일, 모든 gzip 파일 또는 텍스트와 gzip 파일의 조합 이어야 합니다.  
  
-   파일 헤더 정보를 포함할 수 있습니다.  
  
-   모든 파일에는 동일한 문자 인코딩 형식을 사용 해야 합니다. -E 옵션을 참조 하십시오.  
  
-   모든 파일은 동일한 테이블에 로드 되어야 합니다.  
  
-   모든 파일 연결 되며 로드 인 것 처럼 하나의 파일 및 거부 된 행이 단일 거부 파일으로 이동 합니다.  
  
예:  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
로드 오류가 발생 하는 경우 **dwloader** 라는 파일에 오류 정보가 로드 된 후 실패 설명 실패 한 행을 저장 *load_failure_file_name*합니다. 이 파일이 이미 dwloader 기존 파일을 덮어쓰게 됩니다. *load_failure_file_name* 는 첫 번째 오류가 발생할 때 만들어집니다. 모든 행을 성공적으로 로드 하는 경우 *load_failure_file_name* 생성 되지 않습니다.  
  
**-fh** *number_header_rows*  
줄 (행)의 시작 부분에서 무시할 수 *source_data_file_name*합니다. 기본값은 0입니다.  
  
<variable_length_column_options>  
에 대 한 옵션을 *source_data_file_name* 문자 구분 된 가변 길이 열이 있는 합니다. 기본적으로 *source_data_file_name* 가변 길이 열에 ASCII 문자를 포함 합니다.  
  
ASCII 파일에 대 한 Null 구분 기호를 연속적으로 배치 하 여 표현 됩니다. 파이프로 구분 된 파일의 예를 들어 ("|"), NULL을 가리키는 "| |"입니다. NULL을 가리키는 쉼표로 구분 된 파일에 ",". 또한는 **-E** (-emptyStringAsNull) 옵션을 지정 해야 합니다. -E에 대 한 자세한 내용은 아래를 참조 합니다.  
  
**-e** *character_encoding*  
데이터 파일에서 로드할 데이터에 대 한 문자 인코딩 유형을 지정 합니다. 옵션 (기본값) ASCII, UTF8, UTF16, 또는 UTF16BE, 여기서 UTF16 약간 endian 이며 UTF16BE big endian은입니다. 이러한 옵션은 대/소문자 구분.  
  
**-t** *field_delimiter*  
행의 각 필드 (열)에 대 한 구분 기호입니다. 필드 구분 기호에는 이러한 ASCII 이스케이프 문자 또는 16 진수 ASCII 값 중 하나 이상을...  
  
|이름|이스케이프 문자|16 진수 문자|  
|--------|--------------------|-----------------|  
|탭|\t|0x09|  
|캐리지 리턴 (CR)|\r|0x0d|  
|줄 바꿈 (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|쉼표|','|0x2c|  
|큰따옴표|\\"|0x22|  
|작은따옴표|\\'|0x27|  
  
명령줄에서 파이프 문자를 지정 하려면 큰따옴표로 묶습니다 "|"입니다. 명령줄 파서에서 잘못 해석을 피해 야 합니다. 다른 문자는 작은따옴표로 묶여 있습니다.  
  
예:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t '~|~'  
  
**-r** *row_delimiter*  
원본 데이터 파일의 각 행에 대 한 구분 기호입니다. 행 구분 기호는 ASCII 값을 하나 이상.  
  
캐리지 리턴 (CR), 줄 바꿈 (LF) 또는 탭 문자를 구분 기호로 지정 하려면 이스케이프 문자 (\r, \n, \t) 또는 16 진수 값 (0 x, 0d 09)를 사용할 수 있습니다. 구분 기호로 다른 특수 문자를 지정 하려면 해당 16 진수 값을 사용 합니다.  
  
CR LF +의 예:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR의 예:  
  
\r-r  
  
-r 0x0d  
  
LF의 예:  
  
-r \n  
  
-r 0x0a  
  
LF가 Unix 필요 합니다. CR은 Windows 필요 합니다.  
  
**-s** *string_delimiter*  
문자열 데이터에 대 한 구분 기호 텍스트 구분 입력된 파일의 필드를 입력 합니다. 하나 이상의 ASCII 값이 문자열 구분 기호가입니다.  문자로 지정할 수 있습니다 (예:-s *) 또는 16 진수 값 (예:-s 0x22 큰따옴표가 대 한).  
  
예:  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options>  
고정 길이 열이 있는 원본 데이터 파일에 대 한 옵션입니다. 기본적으로 *source_data_file_name* 가변 길이 열에 ASCII 문자를 포함 합니다.  
  
고정된 폭 열-e u t f 8 때 지원 되지 않습니다.  
  
**-w** *fixed_width_config_file*  
경로 각 열에 있는 문자의 수를 지정 하는 구성 파일의 이름입니다. 모든 필드를 지정 해야 합니다.  
  
이 파일 서버를 로드에 있어야 합니다. UNC, 상대 또는 절대 경로 경로일 수 있습니다. 각 줄 *fixed_width_config_file* 해당 열에 대 한 열과 문자 수의 이름을 포함 합니다. 다음과 같이 각 열 마다 한 줄이 고 파일에 순서에는 대상 테이블의 순서와 일치 해야 합니다.  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
고정 너비 구성 파일 예:  
  
SalesCode=3  
  
SalesID=10  
  
예제 라인 *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
이전 예제에서는 로드 된 첫 번째 행을 갖습니다 SalesCode '230' 및 SalesID = = 'Shirts0056'. 두 번째 로드 된 행을 갖습니다 SalesCode'' 줄어들고 SaleID = = 'Towels1356'.  
  
선행 및 후행 공백이 나 데이터 형식 변환 고정된 폭 모드에서 처리 하는 방법에 대 한 정보를 참조 하십시오. [데이터 형식 변환 규칙 dwloader](dwloader-data-type-conversion-rules.md)합니다.  
  
**-e** *character_encoding*  
데이터 파일에서 로드할 데이터에 대 한 문자 인코딩 유형을 지정 합니다. 옵션 (기본값) ASCII, UTF8, UTF16, 또는 UTF16BE, 여기서 UTF16 약간 endian 이며 UTF16BE big endian은입니다. 이러한 옵션은 대/소문자 구분.  
  
고정된 폭 열-e u t f 8 때 지원 되지 않습니다.  
  
**-r** *row_delimiter*  
원본 데이터 파일의 각 행에 대 한 구분 기호입니다. 행 구분 기호는 ASCII 값을 하나 이상.  
  
캐리지 리턴 (CR), 줄 바꿈 (LF) 또는 탭 문자를 구분 기호로 지정 하려면 이스케이프 문자 (\r, \n, \t) 또는 16 진수 값 (0 x, 0d 09)를 사용할 수 있습니다. 구분 기호로 다른 특수 문자를 지정 하려면 해당 16 진수 값을 사용 합니다.  
  
CR LF +의 예:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR의 예:  
  
\r-r  
  
-r 0x0d  
  
LF의 예:  
  
-r \n  
  
-r 0x0a  
  
LF가 Unix 필요 합니다. CR은 Windows 필요 합니다.  
  
**-D** { **ymd** | ydm | mdy | myd |  에서는 dmy | dym | *custom_date_format* }  
입력 열에서 월 (m), (d), 일 및 연도 (y) 모든 날짜/시간 필드에 대 한 순서를 지정합니다. 기본 순서는 ymd 합니다. 같은 소스 파일에 대해 여러 주문 형식의 지정 하려면-dt 옵션을 사용 합니다.  
  
ymd | 에서는 dmy  
ydm 및 dmy 동일한 입력된 형식을 허용합니다. 둘 모두를 시작 또는 끝 날짜의 연도 허용 합니다. 예를 들어 둘 다에 대해 **ydm** 및 **dmy** 날짜 형식, 2013-02-03 또는 2013-03-02 입력된 파일에 있을 수 있습니다.  
  
ydm  
데이터 형식 datetime 및 smalldatetime 열으로 ydm으로 서식이 지정 된 입력만 로드할 수 있습니다. Datetime2, 날짜 또는 datetimeoffset 데이터 형식을 열으로 ydm 값을 로드할 수 없습니다.  
  
mdy  
mdy 허용 <month> <space> <day> <comma> <year>합니다.  
  
Mdy 1975 년 1 월 1 일에 대 한 입력된 데이터의 예:  
  
-   1975 년 1 월 1 일  
  
-   75, 1 월 1 일  
  
-   1 월/1/75  
  
-   01011975  
  
myd  
파일 예제 년 3 월에 대 한 입력 04,2010: 03-2010-04, 4/3/2010  
  
dym  
2010 년 3 월 4 일에 대 한 파일 예제 입력: 04-2010-03, 3/4/2010  
  
*custom_date_format*  
*custom_date_format* 는 사용자 지정 날짜 형식 (예: MM/dd/yyyy)에 대 한 이전 버전과 호환성을 위해서만 포함 합니다. dwloader는 사용자 지정 날짜 형식을 enfoce 하지 않습니다. 대신, 사용자 지정 날짜 형식 지정 경우 **dwloader** ymd, ydm, mdy, myd, dym, 또는 dmy의 해당 설정으로 변환 됩니다.  
  
예를 들어 – D MM/dd/yyyy를 지정 하면 모든 날짜를 월 함께 먼저, 주문 수를 입력 한 일 및 연도 (mdy) 다음 dwloader 필요 합니다. 2 개의 문자 월, 2 자리 일 및 사용자 지정 날짜 형식에 지정 된 대로 4 자리 연도 적용 하지는 않습니다. 다음은 날짜 형식이 – D MM/dd/yyyy 경우에 입력된 파일에 날짜의 형식을 지정할 수는 방법의 예: 01/02/2013, Jan.02.2013, 2013 년 1 월 2 일  
  
보다 포괄적인 서식 지정 정보를 참조 하십시오. [데이터 형식 변환 규칙 dwloader](dwloader-data-type-conversion-rules.md)합니다.  
  
**-dt** *datetime_format_file*  
지정 된 파일에 각 날짜/시간 형식 지정 *datetime_format_file*합니다. 명령줄 매개 변수는 달리 큰따옴표로 공백을 포함 하는 파일 매개 변수가 없습니다 묶어야 합니다. 데이터를 로드 하면 datetime 형식의 변경할 수 없습니다. 원본 데이터 파일 및 대상 테이블에는 해당 열에는 동일한 형식을 가져야 합니다.  
  
각 줄에는 해당 날짜/시간 형식 및 대상 테이블에 있는 열의 이름을 포함합니다.  
  
예:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
준비 테이블을 포함할 데이터베이스 이름입니다. 기본값은 대상 테이블에 대 한 데이터베이스-T 옵션을 지정 된 데이터베이스. 준비 데이터베이스를 사용 하는 방법에 대 한 자세한 내용은 참조 [준비 데이터베이스를 만들](staging-database.md)합니다.  
  
**-M** *load_mode_option*  
추가 upsert, 또는 데이터를 다시 로드할 것인지 지정 합니다. 기본 모드에 추가 합니다.  
  
추가  
로더는 대상 테이블의 기존 행의 끝에 행을 삽입합니다.  
  
fastappend  
로더 대상 테이블의 기존 행의 끝에 임시 테이블을 사용 하지 않고 직접 행을 삽입 합니다. fastappend 다중 트랜잭션 필요 (– m) 옵션입니다. Fastappend를 사용 하는 경우 준비 데이터베이스를 지정할 수 없습니다. 복구 실패 했거나 중단 부하에서은 자신의 로드 프로세스에서 처리 되어야 즉 fastappend와 어떤 롤백이 있습니다.  
  
upsert **-K**  *merge_column* [ ,...*n* ]  
로더는 SQL Server Merge 문을 사용 하 여 기존 행을 업데이트 하 고 새 행을 삽입 합니다.  
  
-K 옵션 병합을 기준으로 열을 지정 합니다. 이러한 열에 고유 행을 표시 해야 하는 병합 키를 형성 합니다. 병합 키에 대상 테이블에 없는 행이 업데이트 됩니다. 대상 테이블에 존재 하지 않으면 병합 키 행이 추가 됩니다.  
  
해시 distributed 테이블에 대 한 병합 키 이거나 배포 열을 포함 합니다.  
  
복제 된 테이블에 대 한 병합 키는 하나 이상의 열 조합 합니다. 이러한 열은 응용 프로그램의 요구에 따라 지정 됩니다.  
  
공백 없이 쉼표로 구분 된 또는 공백을 사용 하 여 쉼표로 구분 된 및 작은따옴표로 묶인 여러 열 이어야 합니다.  
  
원본 테이블에 있는 두 행에 일치 하는 병합 키 값이 있으면 해당 행이 동일 해야 합니다.  
  
다시 로드  
로더는 원본 데이터를 삽입 하기 전에 대상 테이블을 자릅니다.  
  
**-b** *batchsize*  
Microsoft 지원에서 사용 하 여에만 권장 *batchsize* DMS 계산 노드의 SQL Server 인스턴스를 수행 하는 대량 복사에 대 한 SQL Server 일괄 처리 크기입니다.  때 *batchsize* 지정, SQL Server PDW에서 각 부하에 대 한 동적으로 계산 되는 일괄 처리 로드 크기를 재정의 합니다.  
  
SQL Server 2012 PDW 부터는 제어 노드에 동적으로 계산 합니다. 각 부하에 대 한 일괄 처리 크기를 기본적으로 합니다. 이 자동 계산 메모리 크기, 대상 테이블 형식, 대상 테이블 스키마, 유형, 파일 크기 및 사용자의 리소스 클래스 등의 여러 매개 변수를 기반으로 합니다.  
  
예를 들어 FASTAPPEND 로드 모드 고 테이블에 클러스터형된 columnstore 인덱스, SQL Server PDW는 rowgroup를 가리키며 닫힙니다 될 있도록 1,048,576의 일괄 처리 크기를 사용 하려고 하는 기본 및 직접 로드 하 여 columnstore로 이동 하지 않고도 델타 저장소입니다. 메모리에서 1,048,576의 일괄 처리 크기를 허용 하지 않으면, dwloader 더 작은 일괄 처리를 선택 합니다.  
  
부하 형식이 FASTAPPEND는 *batchsize* 그렇지 않은 경우 테이블에 데이터 로드에 적용 됩니다 *batchsize* 준비 테이블로 데이터 로드에 적용 됩니다.  
  
<reject_options>  
로더를 사용 하면 로드 실패의 수를 확인 하기 위한 옵션을 지정 합니다. 로드 실패 임계값을 초과 하는 경우 로더 중단 되 고 모든 행을 적용 하지 됩니다.  
  
**-rt** { **값** | 백분율을 (를)  
지정 여부-*reject_value* 에 **-rv** *reject_value* 옵션은 리터럴 (값) 행 개수 또는 비율 (백분율) 오류입니다. 기본값은 값입니다.  
  
배율 옵션은-rs 옵션에 따라 간격으로 수행 하는 실시간으로 계산 합니다.  
  
예를 들어 100 개 행에서 25 로드 로더 하려고 하면 실패 하는 경우 75 성공 실패율은 25%입니다.  
  
**-rv** *reject_value*  
부하를 중지 하기 전까지 허용 개수 또는 행 거부 사유의 비율을 지정 합니다. **-rt** 옵션 결정 하는 경우 *reject_value* 행 개수 또는 행의 비율을 참조 합니다.  
  
기본 *reject_value* 은 0입니다.  
  
-Rt 값을 사용 하는 경우 거부 된 행 수가 초과 reject_value 로더 부하를 중지 합니다.  
  
-Rt percentage 사용 하는 경우, 로더 간격 비율을 계산 합니다. (-rs 옵션). 따라서 실패 한 행의 비율을 초과할 수 있습니다 *reject_value*합니다.  
  
**-rs** *reject_sample_size*  
함께 사용 된 `-rt percentage` 증분 백분율 검사를 지정 하는 옵션입니다. 예를 들어 1000 reject_sample_size을 사용 하는 경우 1000 행 로드 시도 후 로더 실패 한 행의 비율을 계산 됩니다. 각 추가 1000 개의 행을 로드 한 후 실패 한 행의 비율 다시 계산할 합니다.  
  
**-c**  
Char, nchar, varchar 및 nvarchar 필드의 왼쪽 및 오른쪽에서 공백 문자를 제거합니다. 빈 문자열로 공백 문자만 포함 된 각 필드를 변환 합니다.  
  
예:  
  
' ' 잘리기 때문에 '  
  
'abc'는 'abc' 잘립니다.  
  
-C-E를 함께 사용할 때 – E 작업이 먼저 발생 합니다. 공백 문자만 포함 하는 필드는 NULL이 아닌 빈 문자열인 경우에 변환 됩니다.  
  
**-E**  
빈 문자열을 NULL로 변환 합니다. 기본값은 이러한 변환을 수행 하지 않도록 합니다.  
  
**-m**  
다중 트랜잭션 모드를 사용 하 여 로드;의 두 번째 단계에 대 한 때 분산된 테이블에 준비 테이블에서 데이터를 로드 합니다.  
  
와 **– m**, SQL Server PDW 수행 하 고 동시에 부하를 커밋합니다. 이 기본 모드에서 로드 보다 훨씬 더 빠르게 수행 하지만 트랜잭션 안전 하지 않습니다.  
  
없이 **– m**, SQL Server PDW 수행 하 고 각 계산 노드 내에서 배포 및 동시에 계산 노드에서 부하를 직렬로 커밋합니다. 이 메서드는 다중 트랜잭션 모드 보다 느린 이지만 트랜잭션 안전 합니다.  
  
**-m** 는 선택 사항에 대 한 *추가*, *다시 로드*, 및 *upsert*합니다.  
  
**-m** fastappend에 필요 합니다.  
  
**-m** 복제 된 테이블에 사용할 수 없습니다.  
  
**-m** 두 번째 로드 단계에만 적용 됩니다. 첫 번째 로드 단계;에 적용 되지 않습니다. 준비 테이블로 데이터를 로드 합니다.  
  
다중 트랜잭션 모드에서 복구 실패 했거나 중단 부하에서은 자신의 로드 프로세스에서 처리 되어야 즉 어떤 롤백이 있습니다.  
  
사용 하는 것이 좋습니다 **– m** 데이터 손실 없이 복구할 수 있도록 빈 테이블로 로드 하는 경우에 합니다. 로드 오류를 복구 하려면: 대상 테이블을 삭제, 부하 문제 해결, 대상 테이블을 다시 만드는 및 부하를 다시 실행 합니다.  
  
**-N**  
대상 기기에 신뢰할 수 있는 기관에서 유효한 SQL Server PDW 인증서 확인 합니다. 이 데이터 중이를 통해 공격자가 도난 및 권한이 없는 위치로 전송 합니다. 인증서 어플라이언스에서 이미 설치 되어 있어야 합니다. 인증서를 설치 하려면 지원 되는 유일한 방법은 구성 관리자 도구를 사용 하 여 설치 기기 관리자입니다. 경우 확실 하지 않은 어플라이언스에 설치 된 신뢰할 수 있는 인증서에 있는지 여부 기기 관리자에 게 문의 합니다.  
  
**-se**  
빈 파일을 로드 하지 않고 건너뜁니다. 이 또한 압축을 푸는 작업 빈 gzip 파일을 건너뜁니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
0 (성공) 또는 다른 정수 값 (실패)  
  
명령 창이 나 배치 파일을 사용 하 여 `errorlevel` 반환 코드를 표시 합니다. 예를 들어  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
PowerShell을 사용 하는 경우 사용 `$LastExitCode`합니다.  
  
## <a name="permissions"></a>Permissions  
부하 권한 및 대상 테이블에 적용 가능한 사용 권한 (INSERT, UPDATE, DELETE) 필요합니다. 준비 데이터베이스 만들기 권한이 있으면 (임시 테이블 작성용)이 있어야 합니다. 준비 데이터베이스를 사용 하지 않으면 CREATE 권한이 대상 데이터베이스에 필요 합니다. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>일반적인 주의 사항  
Dwloader를 로드할 때 데이터 형식 변환에 대 한 자세한 내용은 참조 [데이터 형식 변환 규칙 dwloader](dwloader-data-type-conversion-rules.md)합니다.  
  
하나 이상의 공백을 포함 하는 매개 변수, 매개 변수를를 큰따옴표로 묶습니다.  
  
설치 된 위치에서 로더를 실행 해야 합니다. 실행 dwloader 기기와 미리 설치 되어 있고 C:\Program Files\Microsoft SQL Server 데이터 Warehouse\DWLoader 디렉터리에는 있습니다.  
  
매개 변수 파일에 지정 된 매개 변수를 재정의할 수 있습니다 (-f 옵션)를 명령줄 매개 변수로 지정 하 여 합니다.  
  
로더의 여러 인스턴스를 동시에 실행할 수 있습니다. 로더 인스턴스의 최대 수는 미리 구성 된 하 고 변경할 수 없습니다. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
로드 된 데이터 원본 위치에 어플라이언스에서 공간 보다 필요할 수 있습니다. 디스크 사용량을 예측 하는 데이터 하위 집합을 사용 하 여 테스트 import를 수행할 수 있습니다.  
  
하지만 **dwloader** 트랜잭션 프로세스 및 롤백합니다 정상적으로 실패 한 경우, 다시 대량 로드가 완료 되 면 성공적으로 롤백할 수 없습니다. 활성 취소 하려면 **dwloader** CTRL + C를 입력을 처리 합니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
LOG_SIZE는 데이터베이스에 대 한 보다 작아야 하며 모든 동시 로드의 전체 크기는 것이 좋습니다 동시에 발생 하는 모든 부하의 총 크기가 LOG_SIZE의 50% 보다 작은 경우 이 크기 제한을 얻기 위해 큰 부하를 여러 일괄 처리로 분할할 수 있습니다. LOG_SIZE에 대 한 자세한 내용은 참조 하세요. [데이터베이스 만들기](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
하나의 부하 명령 사용 하 여 여러 파일을 로드할 때 모든 거부 된 행은 동일한 거부 파일에 기록 됩니다. 거부 파일 어떤 입력된 파일에는 거부 된 각 행에 표시 되지 않습니다.  
  
빈 문자열은 구분 기호로 사용할 수 없습니다. 빈 문자열은 행 구분 기호로 사용 하는 경우 로드에 실패 합니다. 열 구분 기호로 사용 되는, 부하는 구분 기호를 무시 하 고 계속 기본값을 사용 하 여 "|"으로 열 구분 기호입니다. 문자열 구분 기호로 사용, 빈 문자열은 무시 됩니다. 및 기본 동작이 적용 됩니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
**dwloader** 잠금 동작에 따라 달라 집니다.는 *load_mode_option*합니다.  
  
-   **추가** – 추가 권장 하 고 가장 일반적인 옵션입니다. 준비 테이블로 데이터 로드를 추가 합니다. 잠금 아래에서 자세히 설명 되어 있습니다.  
  
-   **빠른 추가** – 빠른 추가 된 ExclusiveUpdate 테이블 잠금을 수행 하는 최종 테이블에 직접 로드 하 고 준비 테이블을 사용 하지 않는 유일한 모드입니다.  
  
-   **다시 로드** – 다시 로드를 준비 테이블로 데이터를 로드 하 고 준비 테이블 및 최종 테이블 모두에 대 한 배타적 잠금이 필요 합니다. 동시 작업에 대 한 다시 로드 권장 되지 않습니다.  
  
-   **upsert** – Upsert를 준비 테이블로 데이터를 로드 한 다음 최종 테이블을 준비 테이블에서 병합 작업을 수행 합니다. Upsert는 최종 테이블에 대해 배타적 잠금이 필요 하지 않습니다. 성능은 upsert를 사용 하는 경우 달라질 수 있습니다. 사용자 환경에서 동작을 테스트 합니다.  
  
### <a name="locking-behavior"></a>잠금 동작  
**추가 모드 잠금**  
  
추가 (– m 인수 사용) 하는 다중 트랜잭션 모드에서 실행 될 수 있지만 것은 트랜잭션을 안전 하지 않습니다. 따라서 추가 – m 인수 사용) (없이 트랜잭션 작업으로 사용 해야 합니다. 그러나 최종 INSERT SELECT 작업 중 트랜잭션 모드는 여러 트랜잭션 모드 보다 약 6 배 현재 느립니다.  
  
추가 모드의 2 단계로 데이터를 로드합니다. 1 단계를 준비 테이블에 동시에 (조각화가 발생할 수 있습니다.) 소스 파일에서 데이터를 로드 합니다. 2 단계는 최종 테이블을 준비 테이블에서 데이터를 로드합니다. 두 번째 단계에서 수행 된 **INSERT INTO... 선택 WITH (TABLOCK)** 작업 합니다. 다음 표에서 최종 테이블에서 잠금 동작을 보여 줍니다. 및 로깅 동작을 사용 하는 경우 추가 모드:  
  
|테이블 형식|다중 트랜잭션<br />모드 (-m)|테이블이 비어 있지|지원 되는 동시성|로깅|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|힙|예|사용자 계정 컨트롤|예|최소|  
|힙|예|아니오|예|최소|  
|힙|아니요|예|아니요|최소|  
|힙|아니요|아니오|아니요|최소|  
|Cl|예|사용자 계정 컨트롤|아니요|최소|  
|Cl|예|아니오|예|전체|  
|Cl|아니요|예|아니요|최소|  
|Cl|아니요|아니오|예|전체|  
  
위의 표에서 **dwloader** 힙 또는 클러스터형된 인덱스 (CI) 테이블을 다중 트랜잭션 플래그 유무에 로드 하 고 빈 테이블 또는 비어 있지 않은 테이블에 로드 추가 모드를 사용 하 여 합니다. 잠금과 부하의 이러한 조합은 각각의 동작을 로깅 테이블에 표시 됩니다. 예를 들어, (2) 단계와 추가 모드 로드 테이블이 테이블에 대 한 단독 잠금을 만들 PDW 포함할 다중 트랜잭션 모드 하지 않고 클러스터형된 인덱스를 하며이 빈 및 로깅을 최소화 됩니다. 즉, 고객은 빈 테이블에 (2) 단계 및 쿼리를 동시에 로드할 수 없습니다. 그러나 비어 있지 않은 테이블에 동일한 구성을 갖는 로드할 때 PDW 예정 되지 테이블에 대 한 단독 잠금 및 동시성은 가능 합니다. 반면 전체 로깅이 발생, 프로세스를 그대로 유지 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-dwloader-example"></a>1. 간단한 dwloader 예제  
다음 예제에서는의 초기화는 **로더** 만 필요한 옵션을 선택한 상태입니다. 전역 구성 파일에서 사용 되는 다른 옵션 *loadparamfile.txt*합니다.  
  
SQL Server 인증을 사용 하는 예입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
Windows 인증을 사용 하 여 동일한 예입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
오류 파일과 소스 파일에 대 한 인수를 사용 하는 예입니다.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>2. AdventureWorks 테이블에 데이터를 로드 합니다.  
다음 예제는 데이터를 로드 하는 일괄 처리 스크립트의 일부 **AdventureWorksPDW2012**합니다.  전체 스크립트를 보려면 aw_create.bat 파일을 엽니다는 **AdventureWorksPDW2012** 설치 패키지입니다. 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

다음 스크립트 조각 dwloader를 사용 하 여 DimAccount 하 고 DimCurrency 테이블에 데이터를 로드 합니다. 이 스크립트는 이더넷 주소를 사용 하 고 있습니다. InfiniBand, 사용 중이 던 경우 서버 것 *< appliance_name >*`-SQLCTL01`합니다.  
  
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
  
다음은 DimAccount.txt DimAccount 테이블에 로드 하는 데이터가 포함 된 데이터 파일의 예입니다.  
  
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
  
### <a name="c-load-data-from-the-command-line"></a>3. 명령줄에서 데이터를 로드 합니다.  
다음 예제와 같이 명령줄에서 모든 매개 변수를 입력 하 여 스크립트의 예제 B를 바꿀 수 있습니다.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe –S <Control node IP> -E –M reload –e UTF16 -i .\DimAccount.txt –T AdventureWorksPDW2012.dbo.DimAccount –R DimAccount.bad –t "|" –r \r\n –U <login> -P <password>  
```  
  
명령줄 매개 변수 설명:  
  
-   *C:\Program Files\Microsoft SQL Server 병렬 데이터 Warehouse\100\dwloader.exe* dwloader.exe의 설치 된 위치입니다.  
  
-   *-S* 제어 노드의 IP 주소가 옵니다.  
  
-   *-E* NULL로 빈 문자열을 로드 하도록 지정 합니다.  
  
-   *-M 다시 로드* 원본 데이터를 삽입 하기 전에 대상 테이블을 자를 지정 합니다.  
  
-   *-e u t f 16* little endian 문자 인코딩 형식을 사용 하는 원본 파일을 나타냅니다.  
  
-   *-i.\DimAccount.txt* DimAccount.txt 현재 디렉터리에 존재 하는 라는 파일에 데이터를 지정 합니다.  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount* 데이터를 저장할 테이블의 세 부분으로 이루어진 이름을 지정 합니다.  
  
-   *-R DimAccount.bad* 로드 실패가 발생 하는 행 DimAccount.bad 라는 파일에 기록 됩니다.  
  
-   *– t "|"*  DimAccount.txt, 입력된 파일의 필드 파이프 문자로 구분 되어 나타냅니다.  
  
-   *-r \r\n* DimAccount.txt의 각 행을 캐리지 리턴으로 종료 하 고 줄 바꿈 문자를 지정 합니다.  
  
-   *-U < >-P login_name <password>*  로그인과 부하를 수행 하려면 권한이 있는 로그인에 대 한 암호를 지정 합니다.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
