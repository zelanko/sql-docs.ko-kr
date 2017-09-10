---
title: FILEGROUPPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILEGROUPPROPERTY_TSQL
- FILEGROUPPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], property values
- FILEGROUPPROPERTY function
- viewing filegroup properties
- displaying filegroup properties
ms.assetid: b3a930e6-df05-4034-929c-f681f5f6fc6e
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 050ec0b7c3fdc9146a25b1b1f372ee4928d80c09
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  파일 그룹과 속성 이름이 주어졌을 때 지정된 파일 그룹 속성 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FILEGROUPPROPERTY ( filegroup_name , property )  
```  
  
## <a name="arguments"></a>인수  
 *filegroup_name*  
 형식의 식 **sysname** 명명된 된 속성 정보를 반환할 파일 그룹의 이름을 나타내는입니다.  
  
 *속성*  
 형식의 식 **varchar (128)** 반환할 파일 그룹 속성의 이름을 포함 합니다. *속성* 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|반환 값|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|파일 그룹이 읽기 전용입니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsUserDefinedFG**|파일 그룹이 사용자 정의 파일 그룹입니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsDefault**|파일 그룹이 기본 파일 그룹입니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 *filegroup_name* 에 해당 하는 **이름** 열에는 **sys.filegroups** 카탈로그 뷰에 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `IsDefault` 데이터베이스의 주 파일 그룹에 대해 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 속성의 설정을 반환합니다.  
  
```  
  
SELECT FILEGROUPPROPERTY('PRIMARY', 'IsDefault') AS 'Default Filegroup';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Default Filegroup   
---------------------   
1  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [FILEGROUP_ID &#40; Transact SQL &#41;](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [FILEGROUP_NAME &#40; Transact SQL &#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
