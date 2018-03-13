---
title: "bcp를 사용하여 파일 저장 유형 지정(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b3ea3ad1c9c467925e50e4fdc337d2dd99c858b
ms.sourcegitcommit: 657d18fc805512c9574b2fe7451310601b9d78cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2018
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>bcp를 사용하여 파일 저장 유형 지정(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  *파일 저장 유형* 은 데이터 파일에서 데이터가 저장되는 방법을 설명합니다. 데이터는 데이터베이스 테이블 형식(네이티브 형식), 문자 표시(문자 형식) 또는 암시적 변환을 지원하는 모든 데이터 형식의 데이터 파일로 내보낼 수 있습니다. 예를 들어 **smallint** 를 **int**로 복사할 수 있습니다. 사용자 정의 데이터 형식은 해당 기본 형식으로 내보내집니다.  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>파일 저장 유형에 대한 bcp 프롬프트  
 대화형 **bcp** 명령에 **in** 또는 **out** 옵션이 포함된 경우 서식 파일 스위치(**-f**) 또는 데이터 형식 스위치(**-n**, **-c**, **-w**또는 **-N**)가 없으면 각 데이터 필드의 파일 저장 유형을 다음과 같이 입력해야 합니다.  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 이 프롬프트에 대한 사용자 응답은 수행하는 태스크에 따라 다음과 같이 달라집니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터를 최대한 압축된 저장 유형(원시 데이터 형식)의 데이터 파일로 대량으로 내보내려면 **bcp**에서 제공되는 기본 파일 저장 유형을 적용합니다. 네이티브 파일 저장 유형 목록은 이 항목 뒷부분에 있는 "네이티브 파일 저장 유형"을 참조하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터를 문자 형식으로 데이터 파일에 대량으로 내보내려면 **char** 를 테이블의 모든 열에 대한 파일 저장 유형으로 지정합니다.  
  
-   데이터 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스로 데이터를 대량으로 가져오려면 문자 형식으로 저장된 유형에 대해 **char** 를 파일 저장 유형으로 지정하고 네이티브 데이터 형식으로 저장된 데이터의 경우 적절한 파일 저장 유형을 지정합니다.  
  
    |파일 저장 유형|명령 프롬프트에 입력할 내용|  
    |-----------------------|-----------------------------|  
    |**char***|**c**[**har**]|  
    |**varchar**|**c[har]**|  
    |**nchar**|**w**|  
    |**nvarchar**|**w**|  
    |**text***\*|**T**[**ext**]|  
    |**ntext2**|**W**|  
    |**binary**|**x**|  
    |**varbinary**|**x**|  
    |**image***\*|**I**[**mage**]|  
    |**datetime**|**d[ate]**|  
    |**smalldatetime**|**D**|  
    |**time**|**te**|  
    |**date**|**de**|  
    |**datetime2**|**d2**|  
    |**datetimeoffset**|**do**|  
    |**decimal**|**n**|  
    |**numeric**|**n**|  
    |**float**|**f[loat]**|  
    |**real**|**r**|  
    |**Int**|**i[nt]**|  
    |**bigint**|**B[igint]**|  
    |**smallint**|**s[mallint]**|  
    |**tinyint**|**t[inyint]**|  
    |**money**|**m[oney]**|  
    |**smallmoney**|**M**|  
    |**bit**|**b[it]**|  
    |**uniqueidentifier**|**u**|  
    |**sql_variant**|**V[ariant]**|  
    |**timestamp**|**x**|  
    |**UDT** (사용자 정의 데이터 형식)|**U**|  
    |**XML**|**X**|  
  
     \***char** 파일 저장 유형으로 내보낸 데이터 중 문자가 아닌 데이터에 대해 데이터 파일에 할당되는 저장 공간의 크기는 필드 길이, 접두사 길이 및 종결자의 상호 작용에 따라 결정됩니다.  
  
     \*\***ntext**, **text**및 **image** 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이후 버전에서 제거됩니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 응용 프로그램은 수정하십시오. 대신 **nvarchar(max)**, **varchar(max)**및 **varbinary(max)** 를 사용합니다.  
  
## <a name="native-file-storage-types"></a>네이티브 파일 저장 유형  
 각 네이티브 파일 저장 유형은 해당 호스트 파일 데이터 형식으로 서식 파일에 기록됩니다.  
  
|파일 저장 유형|호스트 파일 데이터 형식|  
|-----------------------|-------------------------|  
|**char***|SQLCHAR|  
|**varchar**|SQLCHAR|  
|**nchar**|SQLNCHAR|  
|**nvarchar**|SQLNCHAR|  
|**text***\*|SQLCHAR|  
|**ntext***\*|SQLNCHAR|  
|**binary**|SQLBINARY|  
|**varbinary**|SQLBINARY|  
|**image***\*|SQLBINARY|  
|**datetime**|SQLDATETIME|  
|**smalldatetime**|SQLDATETIM4|  
|**decimal**|SQLDECIMAL|  
|**numeric**|SQLNUMERIC|  
|**float**|SQLFLT8|  
|**real**|SQLFLT4|  
|**int**|SQLINT|  
|**bigint**|SQLBIGINT|  
|**smallint**|SQLSMALLINT|  
|**tinyint**|SQLTINYINT|  
|**money**|SQLMONEY|  
|**smallmoney**|SQLMONEY4|  
|**bit**|SQLBIT|  
|**uniqueidentifier**|SQLUNIQUEID|  
|**sql_variant**|SQLVARIANT|  
|**timestamp**|SQLBINARY|  
|UDT(사용자 정의 데이터 형식)|SQLUDT|  
  
 \*문자 형식으로 저장된 데이터 파일은 **char** 을 파일 저장 유형으로 사용합니다. 그러므로 문자 데이터 파일의 경우 SQLCHAR는 서식 파일에 나타나는 유일한 데이터 형식입니다.  
  
 \*\*DEFAULT 값이 있는 **text**, **ntext**및 **image** 열로 데이터를 대량으로 가져올 수 없습니다.  
  
## <a name="additional-considerations-for-file-storage-types"></a>파일 저장 유형에 대한 추가 고려 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에서 데이터 파일로 데이터를 대량으로 내보내는 경우 다음을 고려하십시오.  
  
-   **char** 를 항상 파일 저장 유형으로 지정할 수 있습니다.  
  
-   잘못된 암시적 변환을 나타내는 파일 저장 유형을 입력하면 **bcp** 가 실패합니다. 예를 들어 **int** 데이터에 **smallint** 를 지정할 수 있지만 **smallint** 를 **int** 데이터에 지정하면 오버플로 오류가 발생합니다.  
  
-   **float**, **money**, **datetime**또는 **int** 와 같이 문자가 아닌 데이터 형식이 데이터베이스 형식으로 저장되면 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 형식으로 데이터 파일에 기록됩니다.  
  
    > [!NOTE]  
    >  **bcp** 명령의 모든 필드를 대화형으로 지정하면 명령에서 비 XML 서식 파일의 각 필드에 대한 응답을 저장하라는 메시지를 표시합니다. 비 XML 서식 파일에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [bcp를 사용하여 필드 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)   
 [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
