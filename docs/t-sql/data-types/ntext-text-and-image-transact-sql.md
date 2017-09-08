---
title: "ntext, text 및 image (TRANSACT-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ntext_TSQL
- ntext
dev_langs:
- TSQL
helpviewer_keywords:
- text data type, about text data type
- text [SQL Server], data types
- ntext data type
- ntext data type, about ntext data type
- image data type, about image data type
ms.assetid: b0d8769c-7598-4f97-8162-ace5f182b5bc
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 76b78b01596b484bc35df1a1e468c5b2bb8ece63
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="ntext-text-and-image-transact-sql"></a>ntext, text 및 image(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

대용량의 유니코드 및 비유니코드 문자와 이진 데이터를 저장하기 위한 고정 및 가변 길이 데이터 형식입니다. 유니코드 데이터는 UNICODE UCS-2 문자 집합을 사용합니다.
  
>**중요!**  **ntext**, **텍스트**, 및 **이미지** 데이터 형식은 나중 버전의 SQL Server에서 제거 됩니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 응용 프로그램은 수정하세요. 대신 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)및 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) 를 사용합니다.  
  
  
## <a name="arguments"></a>인수  
**ntext**  
최대 문자열 길이가 2^30 - 1(1,073,741,823)바이트인 가변 길이 유니코드 데이터입니다. 바이트 단위의 저장소 크기는 입력된 문자열 길이의 두 배입니다. ISO 동의어는 **ntext** 은 **national 텍스트**합니다.
  
**text**  
서버의 코드 페이지에 있는 최대 문자열 길이가 2^31 - 1(2,147,483,647)인 비유니코드 가변 길이 데이터입니다. 서버 코드 페이지에서 더블바이트 문자를 사용하더라도 저장소 크기는 그대로 2,147,483,647바이트입니다. 문자열에 따라 저장소 크기가 2,147,483,647바이트보다 작을 수도 있습니다.
  
**image**  
0에서 2^31-1(2,147,483,647)바이트의 가변 길이 이진 데이터입니다.
  
## <a name="remarks"></a>주의  
다음 함수 및 문을 사용 하 여 **ntext**, **텍스트**, 또는 **이미지** 데이터입니다.
  
|함수|문|  
|---|---|
|[DATALENGTH &#40; Transact SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)|[Readtext&#40; Transact SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)|  
|[PATINDEX &#40; Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)|[SET TEXTSIZE &#40; Transact SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)|  
|[부분 문자열 &#40; Transact SQL &#41;](../../t-sql/functions/substring-transact-sql.md)|[Updatetext&#40; Transact SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[TEXTPTR &#40; Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)|[WRITETEXT&#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[TEXTVALID &#40; Transact SQL &#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)||  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[마찬가지로 &#40; Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)


