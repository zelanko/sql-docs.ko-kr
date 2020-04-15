---
title: 텍스트 파일 형식(텍스트 파일 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5801433e0180bb07cb2d09a59db2bb74be012cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303094"
---
# <a name="text-file-format-text-file-driver"></a>텍스트 파일 형식(텍스트 파일 드라이버)
ODBC 텍스트 드라이버는 구분된 텍스트 파일과 고정 너비 텍스트 파일을 모두 지원합니다. 텍스트 파일은 선택적 헤더 줄과 0개 이상의 텍스트 줄로 구성됩니다.  
  
 헤더 줄은 텍스트 파일의 다른 줄과 동일한 형식을 사용하지만 ODBC Text 드라이버는 헤더 줄 항목을 데이터가 아닌 열 이름으로 해석합니다.  
  
 구분된 텍스트 줄에는 쉼표, 탭 또는 사용자 지정 구분 기호로 구분된 하나 이상의 데이터 값이 포함되어 있습니다. 파일 전체에서 동일한 구분 기호를 사용해야 합니다. Null 데이터 값은 둘 사이에 데이터가 없는 행의 두 구분 기호로 표시됩니다. 구분된 텍스트 줄의 문자 문자열은 이중 따옴표("")로 묶일 수 있습니다. 구분된 값 앞이나 후에 공백이 발생할 수 없습니다.  
  
 고정 너비 텍스트 줄의 각 데이터 항목의 너비는 스키마에 지정됩니다. Null 데이터 값은 공백으로 표시됩니다.  
  
 테이블은 최대 255개의 필드로 제한됩니다. 필드 이름은 64자로 제한되며 필드 너비는 32,766자로 제한됩니다. 레코드는 65,000바이트로 제한됩니다.  
  
 텍스트 파일은 단일 사용자에 대해서만 열 수 있습니다. 여러 사용자가 지원되지 않습니다.  
  
 프로그래머를 위해 작성된 다음 문법은 ODBC 텍스트 드라이버에서 읽을 수 있는 텍스트 파일의 형식을 정의합니다.  
  
|형식|표시|  
|------------|--------------------|  
|비 기울임꼴|그림과 같이 입력해야 하는 문자|  
|*기울임꼴*|문법의 다른 위치에 정의된 인수|  
|대괄호([])|선택적 항목입니다.|  
|중괄호{}()|상호 배타적인 선택 목록|  
|세로 막대(&#124;)|상호 배타적 선택 별도|  
|줄임표(...)|하나 이상 반복할 수 있는 항목|  
  
 텍스트 파일의 형식은 다음과 같은 것입니다.  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  고정 너비 텍스트 파일의 각 열의 너비는 Schema.ini 파일에 지정됩니다.  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  사용자 정의 구분 된 텍스트 파일의 구분 기호는 Schema.ini 파일에 지정 됩니다.  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  구분된 파일의 경우 NULL은 두 구분 기호 간의 데이터 없음으로 표시됩니다.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  고정 너비 파일의 경우 NULL은 공백으로 표시됩니다.
