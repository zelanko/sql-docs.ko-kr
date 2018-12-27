---
title: bcp를 사용하여 파일 저장 유형 지정(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 307cc94aff7fb1e5f8f9bad99aac1c99c08fc293
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048443"
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>bcp를 사용하여 파일 저장 유형 지정(SQL Server)
  *파일 저장 유형* 은 데이터 파일에서 데이터가 저장되는 방법을 설명합니다. 데이터 또는 내보낼 수 데이터 파일에는 데이터베이스 테이블 형식 (네이티브 형식)로 문자 표시 (문자 형식), 암시적 변환이 지원 되는 데이터 형식으로 예를 들어 복사를 `smallint` 으로 `int`합니다. 사용자 정의 데이터 형식은 해당 기본 형식으로 내보내집니다.  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>파일 저장 유형에 대한 bcp 프롬프트  
 대화형 **bcp** 명령에 **in** 또는 **out** 옵션이 포함된 경우 서식 파일 스위치(**-f**) 또는 데이터 형식 스위치(**-n**, **-c**, **-w**또는 **-N**)가 없으면 각 데이터 필드의 파일 저장 유형을 다음과 같이 입력해야 합니다.  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 이 프롬프트에 대한 사용자 응답은 수행하는 태스크에 따라 다음과 같이 달라집니다.  
  
-    [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터를 최대한 압축된 저장 유형(원시 데이터 형식)의 데이터 파일로 대량으로 내보내려면 **bcp**에서 제공되는 기본 파일 저장 유형을 적용합니다. 네이티브 파일 저장 유형 목록은 이 항목 뒷부분에 있는 "네이티브 파일 저장 유형"을 참조하십시오.  
  
-   데이터를 대량 내보내기의 인스턴스로부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문자 형식에서 데이터 파일에 지정 `char` 테이블의 모든 열에 대 한 파일 저장 유형으로 합니다.  
  
-   대량 데이터의 인스턴스를 가져오려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일에서 파일 저장 유형으로 지정 `char` 문자에 저장 된 형식의 서식을 지정 하 고, 네이티브 데이터 형식으로 저장 된 데이터에 대 한 중 하나를 지정 파일 저장소 형식에 적절 하 게 합니다.  
  
    |파일 저장 유형|명령 프롬프트에 입력할 내용|  
    |-----------------------|-----------------------------|  
    |`char` <sup>1</sup>|`c`[`har`]|  
    |`varchar`|`c[har]`|  
    |`nchar`|`w`|  
    |`nvarchar`|`w`|  
    |`text` <sup>2</sup>|`T`[`ext`]|  
    |`ntext2`|`W`|  
    |`binary`|`x`|  
    |`varbinary`|`x`|  
    |`image` <sup>2</sup>|`I`[`mage`]|  
    |`datetime`|**d[ate]**|  
    |`smalldatetime`|`D`|  
    |`time`|`te`|  
    |`date`|`de`|  
    |`datetime2`|`d2`|  
    |`datetimeoffset`|`do`|  
    |`decimal`|`n`|  
    |`numeric`|`n`|  
    |`float`|**f[loat]**|  
    |`real`|`r`|  
    |`Int`|**i[nt]**|  
    |`bigint`|`B[igint]`|  
    |`smallint`|**s[mallint]**|  
    |`tinyint`|**t[inyint]**|  
    |`money`|**m[oney]**|  
    |`smallmoney`|`M`|  
    |`bit`|`b[it]`|  
    |`uniqueidentifier`|`u`|  
    |`sql_variant`|`V[ariant]`|  
    |`timestamp`|`x`|  
    |`UDT`(사용자 정의 데이터 형식)|`U`|  
    |`XML`|`X`|  
  
     <sup>1</sup> 로 내보낸 비문자 데이터에 대 한 데이터 파일에 할당 되는 저장소 공간의 크기를 결정 하는 필드 길이, 접두사 길이 및 종결자의 상호 작용을 `char` 파일 저장 유형입니다.  
  
     <sup>2</sup> 는 `ntext`를 `text`, 및 `image` 데이터 형식의 이후 버전에서 제거 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 애플리케이션은 수정하십시오. 사용 하 여 `nvarchar(max)`하십시오 `varchar(max)`, 및 `varbinary(max)` 대신 합니다.  
  
## <a name="native-file-storage-types"></a>네이티브 파일 저장 유형  
 각 네이티브 파일 저장 유형은 해당 호스트 파일 데이터 형식으로 서식 파일에 기록됩니다.  
  
|파일 저장 유형|호스트 파일 데이터 형식|  
|-----------------------|-------------------------|  
|`char` <sup>1</sup>|SQLCHAR|  
|`varchar`|SQLCHAR|  
|`nchar`|SQLNCHAR|  
|`nvarchar`|SQLNCHAR|  
|`text` <sup>2</sup>|SQLCHAR|  
|`ntext` <sup>2</sup>|SQLNCHAR|  
|`binary`|SQLBINARY|  
|`varbinary`|SQLBINARY|  
|`image` <sup>2</sup>|SQLBINARY|  
|`datetime`|SQLDATETIME|  
|`smalldatetime`|SQLDATETIM4|  
|`decimal`|SQLDECIMAL|  
|`numeric`|SQLNUMERIC|  
|`float`|SQLFLT8|  
|`real`|SQLFLT4|  
|`int`|SQLINT|  
|`bigint`|SQLBIGINT|  
|`smallint`|SQLSMALLINT|  
|`tinyint`|SQLTINYINT|  
|`money`|SQLMONEY|  
|`smallmoney`|SQLMONEY4|  
|`bit`|SQLBIT|  
|`uniqueidentifier`|SQLUNIQUEID|  
|`sql_variant`|SQLVARIANT|  
|`timestamp`|SQLBINARY|  
|UDT(사용자 정의 데이터 형식)|SQLUDT|  
  
 <sup>1</sup> 문자에 저장 된 데이터 파일 형식을 사용 하 여 `char` 파일 저장 유형으로 합니다. 그러므로 문자 데이터 파일의 경우 SQLCHAR는 서식 파일에 나타나는 유일한 데이터 형식입니다.  
  
 <sup>2</sup> 에 데이터를 대량으로 수 없습니다 `text`를 `ntext`, 및 `image` 기본값이 있는 열입니다.  
  
## <a name="additional-considerations-for-file-storage-types"></a>파일 저장 유형에 대한 추가 고려 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에서 데이터 파일로 데이터를 대량으로 내보내는 경우 다음을 고려하십시오.  
  
-   `char`를 항상 파일 저장 유형으로 지정할 수 있습니다.  
  
-   잘못 된 암시적 변환을 나타내는 파일 저장 유형을 입력 하면 **bcp** 실패; 예를 들어 지정할 수 있지만 `int` 에 대 한 `smallint` 데이터를 지정 하는 경우 `smallint` 에 대 한 `int` 데이터 오버플로 오류가 발생 합니다.  
  
-   문자가 아닌 데이터 형식이 같은 경우 `float`, `money`, `datetime`, 또는 `int` 저장 된 데이터베이스 형식으로 데이터를 데이터 파일에 기록 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 형식입니다.  
  
    > [!NOTE]  
    >  **bcp** 명령의 모든 필드를 대화형으로 지정하면 명령에서 비 XML 서식 파일의 각 필드에 대한 응답을 저장하라는 메시지를 표시합니다. 비 XML 서식 파일에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [bcp를 사용하여 필드 길이 지정&#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
