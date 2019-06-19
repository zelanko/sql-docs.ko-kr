---
title: MySQL 및 SQL Server 문자 매핑 (MySQLToSQL)를 설정 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cebdf2ed28287a59ec9d4f0daaa1d0c200f8fe20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312369"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>MySQL 및 SQL Server 문자 집합 매핑(MySQLToSQL)
MySQL 문자 데이터 형식, 식 및 리터럴 문자 집합 (Charset)을 지정할 수 있습니다.  
  
## <a name="charset-mapping"></a>문자 집합 매핑  
문자 집합 매핑 각 MySQL 문자 집합에 대해 정의 되 고 문자 데이터 형식 변환 하는 동안 사용 됩니다. 특정 문자 집합의 문자열 데이터 형식으로 변환 하는 방법을 지정 합니다.  
  
-   National SQL Server 문자 형식 (NCHAR/NVARCHAR) 또는  
  
-   일반 SQL Server 문자 형식 (CHAR/VARCHAR)  
  
1.  **national** 대상 데이터베이스 문자 데이터 형식은:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **일반** 대상 데이터베이스 문자 데이터 형식은:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  형식 매핑 매핑을 허용 **national** 문자 데이터 형식입니다. MySQL 문자 데이터 형식 매핑 형식에 따라 변환 된 후에 문자 집합 매핑이 적용 됩니다.  
  
> [!NOTE]  
> 문자 집합 매핑 메타 데이터 개체 탐색기의 각 노드 수준을 정의할 수 있습니다 및 MySQL에서 읽은 모든 문자 집합을 나타냅니다.  
  
## <a name="charset-mapping-on-different-node-levels"></a>서로 다른 노드 수준에서 문자 집합 매핑  
문자 집합 매핑 다릅니다 다른 노드 수준에서 namely:  
  
1.  루트 메타 데이터 노드 수준에서  
  
2.  데이터베이스, 범주 및 개체 노드 수준  
  
> [!NOTE]  
> 문자 집합 매핑 편집을 위해 선택한 탭에는 다른 노드 수준에서 매핑에 관계 없이 세 가지 단추가 있습니다.  
>   
> 구현되지 않은 것은 다음과 같습니다.  
>   
> 1.  **고려해 야 합니다.** 문자 집합 매핑을 편집 하 고 아직 저장 되지 경우에 사용자가 수행한 변경 내용을 적용 합니다.  
> 2.  **취소:** 사용자가 변경한 내용을 취소 합니다. 문자 집합 매핑 편집 되었지만 저장 되지 경우 단추를 사용할 수 있습니다.  
> 3.  **기본값으로 다시 설정 합니다.** 모든 매핑이 기본값으로 다시 설정합니다.  
  
1.  **루트 메타 데이터 노드 수준:**  문자 집합 매핑 그리드의 각 문자 집합에 대 한 별도 열을 사용 하 여 charset 눈금을 포함합니다. 그리드의 열이 됩니다.  
  
    1.  명명 된 그리드의 첫 번째 열 **문자 집합 이름이** 문자 집합 이름을 포함 합니다.  
  
    2.  명명 된 두 번째 **Charset 설명** charset 설명을 포함 합니다.  
  
    3.  이라는 세 번째 열인 **대상 문자 집합 유형** 특정 문자 집합 매핑 설정이 포함 되어 있습니다. 이 열에 대 한 값은  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 특정 문자 집합에 대 한 기본값을 접두사가 '(기본값)' CHAR/VARCHAR 또는 NCHAR/NVARCHAR 후 합니다.  
  
    MySQL 데이터베이스와 루트 메타 데이터 노드 수준에서 대상 데이터베이스 간의 문자 매핑을 다음과 같습니다.  
  
    ||||  
    |-|-|-|  
    |**문자 집합 이름**|**문자 집합 설명**|**대상 문자 집합 유형 (기본값)**|  
    |big5|중국어 번체 Big5|NCHAR/NVARCHAR (기본값)|  
    |dec8|DEC 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |cp850|DOS 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |hp8|HP 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |koi8r|KOI8-R Relcom 러시아어|CHAR/VARCHAR (기본값)|  
    |라틴어 1|cp1252 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |latin2|ISO 8859-2 중앙 유럽|CHAR/VARCHAR (기본값)|  
    |swe7|7 비트 스웨덴어|CHAR/VARCHAR (기본값)|  
    |ascii|US ASCII|CHAR/VARCHAR (기본값)|  
    |ujis|EUC JP 일본어|NCHAR/NVARCHAR (기본값)|  
    |sjis|일본어 SHIFT-JIS|NCHAR/NVARCHAR (기본값)|  
    |히브리어|ISO 8859-8 히브리어|CHAR/VARCHAR (기본값)|  
    |tis620|TIS620 태국어|CHAR/VARCHAR (기본값)|  
    |euckr|한국어 EUC KR|NCHAR/NVARCHAR (기본값)|  
    |koi8u|KOI8-U 우크라이나어|CHAR/VARCHAR (기본값)|  
    |gb2312|중국어 간체 GB2312|NCHAR/NVARCHAR (기본값)|  
    |그리스어|ISO 8859-7 그리스어|CHAR/VARCHAR (기본값)|  
    |cp 1250|Windows 중앙 유럽어|CHAR/VARCHAR (기본값)|  
    |gbk|GBK 중국어 간체|NCHAR/NVARCHAR (기본값)|  
    |latin5|ISO 8859-9 터키어|CHAR/VARCHAR (기본값)|  
    |armscii8|ARMSCII 8 아르메니아어|CHAR/VARCHAR (기본값)|  
    |utf8|UTF-8 Unicode|NCHAR/NVARCHAR (기본값)|  
    |ucs2|UCS-2 Unicode|NCHAR/NVARCHAR (기본값)|  
    |cp866|DOS 러시아어|CHAR/VARCHAR (기본값)|  
    |keybcs2|DOS Kamenicky 체코어-Slovak|CHAR/VARCHAR (기본값)|  
    |macce|Mac 중앙 유럽어|CHAR/VARCHAR (기본값)|  
    |macroman|Mac 서 부 유럽|CHAR/VARCHAR (기본값)|  
    |cp852|DOS 중앙 유럽|CHAR/VARCHAR (기본값)|  
    |latin7|ISO 8859-13 Baltic|CHAR/VARCHAR (기본값)|  
    |cp 1251|Windows Cyrillic|CHAR/VARCHAR (기본값)|  
    |cp 1256|Windows 아랍어|CHAR/VARCHAR (기본값)|  
    |cp 1257|Windows Baltic|CHAR/VARCHAR (기본값)|  
    |BINARY|이진 의사 문자 집합|CHAR/VARCHAR (기본값)|  
    |geostd8|GEOSTD8 그루지야어|CHAR/VARCHAR (기본값)|  
    |cp932|Windows 일본어 SJIS|NCHAR/NVARCHAR (기본값)|  
    |eucjpms|Windows 일본어 UJIS|NCHAR/NVARCHAR (기본값)|  
  
2.  **데이터베이스, 범주 또는 개체 노드 수준:** 데이터베이스, 범주 또는 개체 노드 수준에서 문자 집합 매핑 표에 루트 메타 데이터 노드 수준에 있는 것과 동일한 행을 시각화 합니다.:  
  
    1.  이라는 그리드의 첫 번째 열 **문자 집합 이름** 문자 집합 이름을 포함 합니다.  
  
    2.  이라는 두 번째 열 **문자 설정 설명** charset 설명을 포함 합니다.  
  
    3.  유일한 차이점은 그리드의 세 번째 열에 있는 값입니다. 이라는 세 번째 열인 **대상 데이터 형식** 특정 문자 집합 매핑 설정이 포함 되어 있습니다. 열에 대 한 값은  
  
        -   상속 (CHAR/VARCHAR 또는 NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   MySQL 데이터베이스와 데이터베이스, 범주 및 개체 노드 수준에서 대상 데이터베이스 문자 집합 매핑, 기본 열에 대 한 루트 이외의 각 수준에서 특정 문자 집합에 대 한 값 **대상 데이터 형식** 해야 ' 상속 된 '.  
> -   값 표의 **상속 된 항목** 하거나 붙음 '(CHAR/VARCHAR)' 또는 '(NCHAR/NVARCHAR)' 값이 특정 문자 집합에서 부모 로부터 상속 된에 따라 합니다.  
  
