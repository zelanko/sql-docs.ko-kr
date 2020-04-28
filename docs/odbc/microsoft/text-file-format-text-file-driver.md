---
title: 텍스트 파일 형식 (텍스트 파일 드라이버) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303094"
---
# <a name="text-file-format-text-file-driver"></a>텍스트 파일 형식(텍스트 파일 드라이버)
ODBC 텍스트 드라이버는 분리 된 텍스트와 고정 너비 텍스트 파일을 모두 지원 합니다. 텍스트 파일은 선택적 헤더 줄과 0 개 이상의 텍스트 줄로 구성 됩니다.  
  
 헤더 줄에서 텍스트 파일의 다른 줄과 동일한 형식을 사용 하지만 ODBC 텍스트 드라이버는 헤더 줄 항목을 데이터가 아닌 열 이름으로 해석 합니다.  
  
 구분 기호로 분리 된 텍스트 줄에는 구분 기호로 구분 된 하나 이상의 데이터 값 (쉼표, 탭 또는 사용자 지정 구분 기호)이 포함 됩니다. 파일 전체에서 동일한 구분 기호를 사용 해야 합니다. Null 데이터 값은 행에서 두 구분 기호 사이에 데이터를 표시 하지 않습니다. 구분 기호로 분리 된 텍스트 줄의 문자열은 큰따옴표 ("")로 묶을 수 있습니다. 구분 기호로 분리 된 값 앞 이나 뒤에 공백이 있을 수 없습니다.  
  
 고정 너비 텍스트 줄의 각 데이터 항목 너비가 스키마에 지정 됩니다. Null 데이터 값은 공백으로 표시 됩니다.  
  
 테이블은 최대 255 필드로 제한 됩니다. 필드 이름은 64 자로 제한 되며 필드 너비는 32766 자로 제한 됩니다. 레코드는 65000 바이트로 제한 됩니다.  
  
 텍스트 파일은 단일 사용자에 대해서만 열 수 있습니다. 여러 사용자가 지원 되지 않습니다.  
  
 프로그래머를 위해 작성 된 다음 문법은 ODBC 텍스트 드라이버에서 읽을 수 있는 텍스트 파일의 형식을 정의 합니다.  
  
|형식|표시|  
|------------|--------------------|  
|비 기울임꼴|표시 된 대로 입력 해야 하는 문자|  
|*기울임꼴*|문법의 다른 위치에 정의 된 인수|  
|대괄호 ([])|선택적 항목입니다.|  
|중괄호 ({})|상호 배타적인 선택 목록|  
|세로 막대 (&#124;)|함께 사용할 수 없는 별도의 선택 항목|  
|줄임표(...)|한 번 이상 반복 될 수 있는 항목|  
  
 텍스트 파일의 형식은 다음과 같습니다.  
  
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
>  고정 너비 텍스트 파일에서 각 열의 너비는 schema.ini 파일에 지정 됩니다.  
  
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
>  사용자가 구분한 텍스트 파일의 구분 기호는 schema.ini 파일에 지정 됩니다.  
  
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
>  구분 된 파일의 경우 NULL은 두 구분 기호 사이에 데이터가 없음을 나타냅니다.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  고정 너비 파일의 경우 NULL은 공백으로 표시 됩니다.
