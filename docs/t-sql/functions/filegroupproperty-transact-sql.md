---
title: FILEGROUPPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6cdc7d89b93d8961ed6000efdef4b34c34a54a7d
ms.sourcegitcommit: 90a9a051fe625d7374e76cf6be5b031004336f5a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39228409"
---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수는 지정한 이름 및 파일 그룹 값에 대해 파일 그룹 속성 값을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FILEGROUPPROPERTY ( filegroup_name, property )  
```  
  
## <a name="arguments"></a>인수  
 *filegroup_name*  
명명된 속성 정보를 반환하는 `FILEGROUPPROPERTY`의 파일 그룹 이름을 나타내는 **sysname** 형식의 식입니다.  
  
 *property*  
파일 그룹 속성의 이름을 반환하는 **varchar(128)** 형식의 식입니다. *Property*는 다음 값 중 하나를 반환할 수 있습니다.  
  
|값|설명|반환 값|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|파일 그룹이 읽기 전용입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsUserDefinedFG**|파일 그룹이 사용자 정의 파일 그룹입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 잘못된 입력|  
|**IsDefault**|파일 그룹이 기본 파일 그룹입니다.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 잘못된 입력|  
  
## <a name="return-types"></a>반환 형식  
**int**  
  
## <a name="remarks"></a>Remarks  
*filegroup_name*은 **sys.filegroups** 카탈로그 뷰의 **name** 열과 일치합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 `IsDefault` 데이터베이스의 주 파일 그룹에 대해 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 속성 설정을 반환합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [FILEGROUP_ID&#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [FILEGROUP_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
