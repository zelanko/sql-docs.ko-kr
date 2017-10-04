---
title: "외부 파일 형식 (Transact SQL) DROP | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cf9009b-59f9-4aac-bef1-dcf2cf0708b2
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 25719f7617cbb75b1b9467a00c392f703a9710ac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-file-format-transact-sql"></a>DROP 외부 파일 형식 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 외부 파일 형식을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Drop an external file format  
DROP EXTERNAL FILE FORMAT external_file_format_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *external_file_format_name*  
 삭제 하는 외부 파일 형식의 이름입니다.  
  
## <a name="metadata"></a>메타데이터  
 외부 파일 형식 사용 하 여의 목록을 보려면는 [sys.external_file_formats&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md) 시스템 뷰.  
  
```  
SELECT * FROM sys.external_file_formats;  
```  
  
## <a name="permissions"></a>Permissions  
 필요한 외부 파일 형식을 변경 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 외부 파일 형식 삭제 해도 외부 데이터는 제거 되지 않습니다.  
  
## <a name="locking"></a>잠금  
 외부 파일 형식 개체에 대 한 공유 잠금을 사용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-basic-syntax"></a>1. 기본 구문을 사용 하 여  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-basic-syntax"></a>2. 기본 구문을 사용 하 여  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  


