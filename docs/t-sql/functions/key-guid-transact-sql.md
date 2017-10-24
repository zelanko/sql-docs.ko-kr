---
title: KEY_GUID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Key_GUID_TSQL
- Key_GUID
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], GUIDs
- KEY_GUID function
- GUIDs [SQL Server]
ms.assetid: 9246c7b2-7098-42c4-a222-cbf30267c46a
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e167366e86cf10403abc6cafa894ad964c60733
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="keyguid-transact-sql"></a>KEY_GUID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스에 있는 대칭 키의 GUID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
Key_GUID( 'Key_Name' )  
```  
  
## <a name="arguments"></a>인수  
 **'** *Key_Name* **'**  
 데이터베이스에 있는 대칭 키의 이름입니다.  
  
## <a name="return-types"></a>반환 형식  
 **uniqueidentifier**  
  
## <a name="remarks"></a>주의  
 키를 작성할 때 ID 값을 지정한 경우 키의 GUID는 해당 ID 값의 MD5 해시입니다. 지정된 ID 값이 없는 경우 서버가 GUID를 생성합니다.  
  
 임시 키의 경우 키 이름이 숫자 기호(#)로 시작해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 임시 키는 생성된 세션에서만 사용할 수 있으므로 액세스 권한이 필요 없습니다. 임시 키가 아닌 키에 액세스하려는 호출자는 키에 대한 일부 권한이 필요하며 키에 대한 VIEW 권한이 거부되어서는 안 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `ABerglundKey1`이라는 대칭 키의 GUID를 반환합니다.  
  
```  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  

